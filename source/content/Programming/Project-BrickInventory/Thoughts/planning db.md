---
title: "Planning it out: the DB Schema"
created: 22, Jan, 2025
modified:
  - 23, Jan, 2025
  - 22, Jan, 2025
---

> [!note] Stream of Consciousness

Before diving into setting up the repo and project files, I figured I'd take a page out of the Capstone book and do a little planning.

The make or break of applications like these tends to be the database structure, so the more I can figure out ahead of time, the easier it'll be to do the CRUD (Create, Read, Update, Delete) operations.

## Schema v0.1

There's 2 major *objects* that come to mind when thinking about Legos:

- sets
- pieces

Sets can be big or small and sometimes consist of other sets, and are denoted by a number. Pieces are a bit more tricky because of the amount of variance. Just listing out some properties should give a good idea of the complexity:

- blocks
	- footprint
	- headprint
	- volume?
	- graphic?
	- shape?
		- rect
		- circ
	- color
		- transparency
	- extrusion

- sets
	- theme/setting
	- subsets
	- parts

- special?
	- handheld?
		- lightsaber
		- radio
	- character accessories?
		- hats
		- tools
		- weapons
		- etc

### Blocks

The first thing that comes to mind is the difference between a 2x2 slanted piece: 

> "is the slant downwards or upwards?"

And that's where the thought about recording the dimension for both the `footprint` and "`headprint`" comes into play. Consider the two slanted blocks:

- Block 1 (slanted downward)
	- footprint: 2x2
	- headprint: 1x2
- Block 2 (slanted upward)
	- footprint: 1x2
	- headprint: 2x2

On one hand, I want to say this kind of detail is overkill, but on the other, Lego has like hundreds of thousands (if not millions) of pieces at this point; so, being able to filter pieces by their physical properties is going to help out a lot.

This naturally leads to `volume` and `extrusion`. `height` might be a more applicable property than `volume` but the idea is to help differentiate between a `fp: 1x2, hp: 1x2` of height 1 and of height 6. 

If I go the `height` route, I can almost get rid of `extrusion`- as the idea here was to specify `flat` or `not` (better term?). The trick is then, what value corresponds to one of those `flat` pieces? I think technically it takes about 3 of them to equal one block height, but storing floats/fractions doesn't feel ideal. I could technically list it as `0` but then map that in the UI to say "flat". It might be a small pain, but its probably easier to understand than dealing with `volume` and `extrusion`.

`color` is pretty easy, with the note that there are transparent blocks. I don't recall any variance in the levels of transparency but that may have changed over the years. For now `transparency` could be a simple boolean. `graphic` is also somewhat straightforward: 

>"is there a graphic printed onto the block?"

The slightly tricky bit, is whether or not to internally try and categorize the graphics. I'm tempted to say no, because with the amount of filters, you should be able to narrow things down significantly (especially with color), and then you are just searching through a relatively small list of similar blocks, looking for the correct one.

And finally, we have `shape`. Again, might be able to get rid of it, but being able to eliminate a whole subcategory of block types would be pretty powerful: I'm thinking of the `1x1x1` cylinders vs `1x1x1` rectangles. This one might be on the chopping block once the data is populated, if the other options sufficiently narrow the possibilities enough.

### Sets

There's really only four things I can think of for sets:

- Set number
- the theme/setting (e.g. Hogwarts vs the old Medieval sets)
- subsets (big box that contains smaller sets)
- parts

Subsets, parts, and the set number are all pretty static in that I'm not seeing really any way or reason to try and expand/shrink the properties.

Storing the theme/setting might be an interesting problem. What I would like to avoid is having a big theme/setting table like:

| Set Number | Hogwarts | Rescue Squad | Octane | etc |
| --- | -- | -- | -- | --- |
| xxxxx | 1 | 0 | 0 | 0 | 0 |
| xxxxy | 0 | 1 | 1 | 0 | 0 |

and so on...

In the program/interface, I think I'd ideally want them to work like tags? especially when it comes to more of the "themes" part of it. I might have to take a peak at how internally Lego handles sorting their sets: do they separate theme from setting, only do one of them, or both?

### Special

This one is going to be rough... In a sense, its the worst outcome: the catch-all for anything that doesn't fit into the `block` structure. Examples that come to mind are:

- lightsabers
- weapons
- radios/tools
- hats/hair
- capes
- weird set specific pieces

And ultimately, there might not be a way around needing this one, and, unfortunately, I'm not sure how to really structure it in a meaningful way.

Two main categories stand out though:

- hand held pieces (like the tools/weapons)
- wearables (hats/hairs/capes/armor)

That might just have to do for now, but I can already tell that searching for a "special" piece to add to a set would be painful. That said, I could try adding *some* descriptors like `color` - at least that way, if you know the radio is black, you only have to search for a `handheld` piece that has `color: black`.

### Tables

The easy part is that I know I need at least three tables. The question which I need to think about over some coffee is... how many sub-tables do I create?

E.g.: does `color` get its own table? or do I just store strings directly?

..

Oh right! I need to have a space for recording current inventory.

..

Okay, relisting the table properties I have so far:

> Blocks:

| PartNumber | Footprint | Headprint | Height | Color    | Graphic | Shape    | InventoryCount |
| ---------- | --------- | --------- | ------ | -------- | ------- | -------- | -------------- |
| int        | string    | string    | int    | ColorKey | bool    | ShapeKey | int            |

> Sets:

| SetNumber | Setting | IsSubset | SubsetOf | InventoryCount |
| --------- | ------- | -------- | -------- | -------------- |
| int       | string  | bool     | int      | int            |

> PartsInSet:

| SetNumber | PartNumber | Quantity |
| --------- | ---------- | -------- |
| int       | int        | int      |

> Special:

| PartNumber | IsHandheld | IsWearable | Description |
| ---------- | ---------- | ---------- | ----------- |
| int        | bool       | bool       | string      |

Thinking about it, I can really just add the three columns of the `Special` table to `Blocks`. 

## Wrap up

If I remember my terminology correctly, the following is the database in "second normal form":

![[Programming/Project-BrickInventory/SchemaV01_SecondNormalForm.png]]

Technically, Transparent depends on Color, so to achieve "third normal form", we'd make: 

> Colors

| ColorKey | Name   | IsTransparent |
| -------- | ------ | ------------- |
| int      | string | bool          |

Although, that being said... its not like only specific colors can be transparent, so you could argue that the transparency doesn't depend on color and call the above implementation "third normal form". In a growing and changing system, I would opt to make the additional table.

In the actual implementation stage, I might opt to split `footprint` and `headprint` into their subjective components: `width` and `length`. I'm not sure, but I feel like I remember hearing something in one of my database classes about the string comparisons being more costly than simpler types, so an optimization would be to convert them to their integer counterparts.