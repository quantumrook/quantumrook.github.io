---
title: "1. Planning it out: the Flow"
created: 23, Jan, 2025
modified:
  - 11, Feb, 2025
  - 23, Jan, 2025
---
>[!note] Stream of Consciousness

Alright, next on the table is the flow of the program or "user stories".

There's two main phases of use:

- Initial inventory & Setup
- Managing

In the idealized situation, the database would already have all of the data for every possible block that Lego has produced. This means the user would only be creating records for the sets they own (and possibly the pieces that belong to that set).

## Add Set

From the schema, we know the user needs to provide 3 pieces of information:

- the SetNumber
- Is it a Subset and of which Set?
- How many they have

So that's six controls:

- textbox for SetNumber
	- only allow integers
- checkbox for "Is Subset?"
	- default to unchecked
- textbox for Main Set
	- disabled if checkbox is not checked
	- only allow integers
- textbox for Inventory Count
	- only allow integers
	- default to 1?
- button for Add
	- default to disabled
- button for Cancel


> [!warning] I need to verify that Lego's Set numbers are purely numeric

Other than that, we can do validation checking either on input changing or once "has focus" is no longer true. Personally, I'm more of a fan of the "as input changes" approach and then once all fields report valid inputs we can enable the add button.

### Conflicting Set Number

Things to consider are:

- What if there's already an entry with that set number?
	- We'd need to check the list of sets before attempting to create the new record
	- Do we update?
	- Do we deny?

The simplest approach is probably to respond with an error that the set already exists. The more intuitive/"useful" approach is to probably kick back a message that says:

> "This set already exists in the database, would you like to update using the new information?"
> 
> And then show what currently exists.

*In theory*, this should be easy to do, as I imagine the main view to consist of sets entered, so we should have recently fetched the relevant information from the database - which means no extra query: we just need to find the match and display it in a readable format.

### On Cancel

- Do we save the inputted information in variables (but not commit to the DB)?
	- This makes an "oops I accidentally clicked cancel/close" faster to recover from
	- Would only store during runtime, and clear out once a set has been added

Could be a nice quality of life feature, but I'd need to figure out a way for the variables to persist between creation of windows, and that means changing their scope.

### Add multiple sets?

Something to consider is the option for the user to somehow specify they're trying to add a number of sets in bulk - most likely use case would be adding the sub-sets all at once.

- is this a different window?
- is this just a flag that's set when triggering the "Add Set" functionality?
	- if `flag=true` then pre-populate `Is Subset` and `Main Set` with previous information

## Edit Set

What do we allow to be changed?

The easiest case is for the user going "Oh, *this* set is actually a sub-set of *that* set", but there's also the chance that they mistyped the SetNumber.

Need to have the same behaviour for conflicting SetNumbers as in the adding step - for consistent experience.

### Edit multiple?

## Remove Set

The big question here is: If the set in question is a Main Set, do we

- remove all subsets
- just remove the main set

The approach probably is to notify the user that the set in question is a Main Set and show the subsets. Then ask if they would like to also remove the subsets.

- if yes, we remove the main and sub sets
- if no, change the subsets to be main sets

This one is important to do in the right order, we don't want orphaned data.

- Remove the sub-set entry from `PartsInSet`
- Remove the sub-set entry from `Sets`
- Remove the main-set entry from `Sets`

## Update Part Inventory
### Blocks: InventoryCount

> [!note] Sidenote:
> 
> I think I might actually need a fourth table: `PartsInSet->Quantity` should specifically be how many of that part is in the set, according to the directions. That means I need another table which is something like `InventoryOfPartsInSet->Quantity` which is how many of the block in question the user has for that set.
> 
> Then again, I could actually just add a fourth column to `PartsInSet` which is `Total`.

This UI would functionally be the same as if we were creating one for "Adding Parts" to the database:

- textfield for PartNumber?
	- disabled and just the autoincrement from the table?
- textfield/dropdown for Footprint
- textfield/dropdown for headprint
- textfield/dropdown for height
- dropdown for color
- checkbox for transparency
- checkbox for graphic
- dropdown for shape
- textfield for InventoryCount
- checkbox for IsHandheld
- checkbox for IsWearable
- textfield for description

What we could do is have footprint/headprint be not required if `isHandheld` or `isWearable` are checked, as well as `shape`, `graphic`, and `height`.

I'm not sure whether or not PartNumber should even be visible? I mean, if we had *the ultimate Lego database* to reference, then having that information to show would be helpful, but other than that, I think its just an internal database property?

The use of dropdowns would be useful in ensuring (and communicating) the input is possible and avoids the issues of like: "Did I specify footprint as 2x2 or 2,2?" but that means it needs to populate from somewhere... which probably should just exist in a table, instead of generating it at runtime.

> Actually, do we even want `InventoryCount` to be changed?

The thing is: you might have parts but no set for them, or extra parts - then `InventoryCount` will be greater than the sum of `PartsInSet:Quantity` for the corresponding `PartNumber`. That's okay, but what do we do if the changed value for `InventoryCount` is now **less** than the sum of `PartsInSet:Quantity?

It's possibly a bit of work, but the "correct" thing to do would then display the list of sets that have the corresponding part and prompt the user to update `PartsInSet:Quantity` until the sum is equal to `InventoryCount`.

That means we need to have a check happen before updating the record and conditionally fetch the `PartsInSet` and possibly even `Sets` information to help the user understand what they're looking at: as in, I don't expect them to remember off the top of their head what set is which.

>[!note] Sidenote
>
>I probably should add an optional field of `Description` to the `Sets` table as well.

### PartsInSet: Quantity

We might almost want to just reuse the window that would be created above (re: handling `InventoryCount < Sum(PartsInSet:Quantity)`).

And honestly, that's probably the best move, as you could also handle the control flow of "well, I'm only missing 1 `block` for set `xxxx` and I only have 1 of 5 for set `yyyy`, so let me just redistribute."

## Assign Parts to Set

This one should probably be the simplest? We need:

- Dropdown for SetNumber
- Dropdown for PartNumber
- textfield for Quantity
- textfield for Total

Although, that being said: am I really going to force someone to remember what PartNumber corresponds to what block? I would also have to expose PartNumber then. So...

We need a way to filter blocks such that they can choose the correct one and then map that choice to PartNumber. Which means... we need all the controls for adding a part so they can be used as filters:

- dropdown for footprint, headprint, height, color, shape
- checkboxes for transparent, graphic, is handheld, is wearable
- textbox to display description

This... is probably going to be one of the most complicated views. We also probably want to go the extra mile and display what we currently have for parts associated with the set (and information about the set).

---

The only flow that is really missing from above is "Adding a Part" from scratch, but I think I'm going to operate under the *idealized* situation for now and assume the database will always have every possible part in it, and then revisit this user action later.

## ToDo: 

### Database Schema changes

- Add tables for: `footprint`, `headprint`, `height`, `color`, and `shape`
	- To populate dropdown menus
- Add `Total` to `PartsInSet`
- Add `Description` to `Sets`