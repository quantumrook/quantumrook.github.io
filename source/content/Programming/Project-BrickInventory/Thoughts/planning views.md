---
title: "2. Planning it out: the Views"
created: 23, Jan, 2025
modified:
  - 11, Feb, 2025
  - 23, Jan, 2025
---
> [!note] Stream of Consciousness

The big question:

> How much information do we want to show to the user?

'Cause there's definitely the approach that uses table views (or tree views? I forget the name of the control) where we do something like:

![[Programming/Project-BrickInventory/OverviewView.png]]

But then this still doesn't cover everything such as showing which sets are missing what parts (or what sets are complete or vice versa).

So, this gives rise to two(?) main view types:

- inventory
- stock/satisfaction

and most likely some sort of overview which gives insight into both?

I think the default being the stock/satisfaction page is probably the most useful, as you'd open the application most often (in the management phase) to see where you are and/or to update `PartsInSet:Quantity`.

I'm feeling drawn to the notebook or tabbed view control for this, as we can easily separate the two different types of information.

## Tab 1: Inventory

This tab will be the easiest to populate with information, since (at least in its current form) its just the two main tables from the database. From [[Programming/Project-BrickInventory/Thoughts/planning flow|Planning the Flow]], we can easily separate those control paths into a series of buttons for each section:

- Sets
	- Add Set
	- Edit Set
	- Remove Set
- Parts
	- Assign Parts to Set
	- Update Part Inventory

On the other hand, it might be more useful to have that second part of the page (labeled "Parts" in the image above) as displaying the only the parts relevant to a selected set. However, that starts crossing over into the stock/satisfaction view.

>Maybe we'll ultimately collapse the two separate views into one, but noticing simplifying behaviour like this?

One important consideration is going to be the managing and displaying of parts in the Part table view: there's going to be a *ton* of blocks in the idealized database case. First thing we can do is opt to only show non-zero `InventoryCount` blocks, and the next thing would probably be to only show 20 at a time.

In addition to the controls for the flows listed above, we probably also want toggles (radiobuttons/checkboxes/dropdowns) for filtering what to display.

A nice quality of life feature might be to:

1. Save the current view when exiting
2. Save the current filters when exiting

So on launch, the program defaults to what was last being looked at (and any applicable filters active).

## Tab 2: Stock/Satisfaction

Actually, this one isn't going to be as bad as I thought, since its really just the result of the `PartsInSet` table.

Ideally it'd be grouped by set (and maybe even sub-sets grouped by main set) and then list the part number, its description and then the `Quantity` and `Total`. Filters for showing specific sets and/or parts that are satisfied/not satisfied.

## Windows

And then that just leaves little windows for the user stories (or flows as I've been calling them). I already have most of that logic thought out in [[Programming/Project-BrickInventory/Thoughts/planning flow|Planning the Flow]], so I'll opt to not repeat myself.

It looks like about six windows will be necessary? But depending on design, I might be able to simplify that down by including some of the information for resolving conflicts or questionable situations on the relevant window (versus making another window to handle the edge cases).
