---
title: "3. Planning it out: the Architecture"
created: 23, Jan, 2025
modified:
  - 11, Feb, 2025
  - 23, Jan, 2025
---
>[!note] Stream of Consciousness

Alright, last but not least: the general organization of the project and logic. The most straightforward approach seems to be:

- the UI layer
- the DB interaction layer
- the mediator

Somewhat self explanatory, but the logic for validating input, displaying controls, and handling behaviour would all be located in the UI section. Actual query construction and fetching results would be the DB interaction layer (also should deal with an necessary joins). Then the big complex part is going to be the mediator which needs to manage the connection to the database, convert data into UI friendly object/structures, convert changed object/structures into update/remove queries, and finally: convert UI control values into parameters to be used by the DB layer for queries.

Which... is much easier said than done.

## Tools for the job:

Nothing immediately screams out "hey, use inheritance here!", so that should simplify some stuff. I probably want to make an interface for the object/structures going in/out of the database, but I guess that depends on what behaviour I want those to ultimately have: e.g. are they just data structures or do they also *do* things?

If I recall correctly, there's either a built-in or well maintained package/library for handling SQL, which is probably overkill (especially because there's not really any security concerns with this program: its not managing any sensitive information, no payments, no PII, no external connections), but having something well tested is more streamlined than reinventing a query-building-wheel. Maybe I'll look into spinning my own just for fun after the big steps are done.

There might actually be a OOP design pattern called "the mediator", I'll have to look into that to make sure I'm not horribly butchering concepts. If it does exist and does what I'm referring to it as doing (as noted above), then I'll go ahead and follow that pattern for as long as it makes sense. If not, then I don't think this use case *specifically* requires a design pattern, but I'm probably indirectly going to be using some or parts of them along the way.

> I do remember "MVC" - Model, View, Controller - being a thing, but I think I had issues mentally mapping out exactly how it worked. Might be a case where the given example was a bit too contrived or didn't properly show how well it could be leveraged.
> 
> I know there's a benefit in separating the logic out, but what comes to mind was a bunch of repeated code. Again, most likely a problem with the example. Maybe I'll look into it again as this project evolves.

I'll actually have to check VisualStudio itself (or maybe a quick search): I remember WinForms being the handy GUI that Microsoft gave us to work with, but that's almost 10 year old technology at this point. I imagine they've created a new thing, I think WPF(?) was supposed to be the replacement alongside Windows 10 but I don't know if that actually got off the ground or if there's a new GUI package or if its still good ol' WinForms.

WinForms would technically be nice, since I have experience with it, but given how things worked with tkinter in [[Programming/Project-Empyrean/About|Project Empyrean]], I feel fairly confident if I have to tackle something new.

I'm probably forgetting *something* but short of using UML (?) to more specifically mock out user stories/flows I think I've hit everything I can at this stage and the next step is to create a repo and fire up VisualStudio.

> I guess this probably is the UML step, but it did just occur to me that I could plan a bit further by trying to mock out some of the flows to get an idea of what classes I'd create and who would be responsible for what.
> 
> There's a point though, where its better to just start getting your hands dirty so you can actually see what you're dealing with instead of the idealized version. And the immediate contra to that statement is: if you have a better idea of what is responsible for what actions/logic, you can strive to better maintain that separation as you build it out.
