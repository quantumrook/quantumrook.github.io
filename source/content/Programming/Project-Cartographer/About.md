---
title: About Project Cartographer
created: 02, Jan, 2025
modified:
  - 02, Jan, 2025
---
> TODO: upload source code

Project Cartographer was the python project I created for my undergraduate thesis. The gist is I made a series of scripts that would used [matplotlib](https://matplotlib.org/) to generate animations for the trajectory of objects transiting near a [Schwarzschild black hole](https://en.wikipedia.org/wiki/Schwarzschild_metric).

One of the goals of the project was to leverage a pathfinding algorithm to navigate a simulated spacetime grid to find the paths within a specified tolerance to avoid usage of methods like the 
[Verlet](https://en.wikipedia.org/wiki/Verlet_integration) or the [Euler](https://en.wikipedia.org/wiki/Euler_method) methods to determine an object's future location.

Moderate success was achieved with a static spacetime grid and the animations and visualizations received praise from fellow undergraduates for assisting in understanding movement in the spacetime.

On the todo list is to refactor the code using a dynamic grid to improve the pathfinding performance and reduce deviation from the plotted Verlet and Euler methods.

## Static vs Dynamic Spacetime Grids

> What do I mean by this?

The current implementation, a static grid, is your typical 2-dimensional array creating a mesh for the spacetime. The vertices are at uniform step sizes in `x` and `y` (converted to `r` and $\phi$ to better reflect the symmetry).

For a flat spacetime (like [Minkowski](https://en.wikipedia.org/wiki/Minkowski_space)), this would be perfect, but because Schwarzschild spacetime has [curvature](https://en.wikipedia.org/wiki/Curved_spacetime) (due to the singularity at the origin), the static grid step size does a poor job at handling the increasing spacetime separation as one nears the [event horizon](https://en.wikipedia.org/wiki/Event_horizon). Or, put another way, the pathfinding algorithm has to make steeper/bigger steps from node to node as the object nears the event horizon, because there isn't a closer node that matches the potential the object would have.

Depending on initial conditions, this can lead to unphysical results such as the object escaping (leaving orbit of the black hole) or being captured, when it otherwise shouldn't.