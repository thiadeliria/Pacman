## Overview
**Summary:** a Python implementation of AI search algorithms to solve problems within the Berkeley Pac-Man environment. The [Pac-Man Projects, developed at UC Berkeley](http://ai.berkeley.edu), apply AI concepts to the classic arcade game Pac-Man. The code uses Python 2.7.13 plus NumPy 1.13.1 and SciPy 0.19.1.

**Concepts:** uninformed and informed state-space search, probabilistic inference, reinforcement learning.

## How to Play
Use WASD or arrow keys to control Pac-Man. To start an interactive game, type at the command line:

`python pacman.py`

<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_default.gif" width="540" />


To see how Pac-Man fares using search algorithms, we can define some variables:

`python pacman.py -l MAZE_TYPE -p SearchAgent -a fn=SEARCH_ALGO` where `MAZE_TYPE` defines the map layout, and `SearchAgent` navigates Pac-Man through the maze according to the algorithm supplied in the `SEARCH_ALGO` parameter.


## Uninformed Search
Given the inputs:
* initial state - the maze cell that Pac-Man starts in,
* successor function - possible actions that he can take (*e.g.*, *move east*), and
* goal state - the cell that he wants to be in,

the search algorithm returns a sequence of states that leads Pac-Man from initial to goal state. The strategy is to iteratively generate a list of successor states (called the *frontier*) until a path to the goal state is found. 

### Depth-First Search vs. Breadth-First Search
<img align="right" src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_tinymaze.png" width="200" />

We can compare some algorithms by observing how Pac-Man fares on a tinyMaze `MAZE_TYPE` with a fixed food dot.

Pac-Man's current position, the upper right corner of the map, is the initial state. His goal state is the cell in the lower left corner that contains a food dot. The search algorithm will make a queue of un-explored cells for Pac-Man to visit in order.

#### Depth-First Search (DFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs` and get:

<img align="left" src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_dfs.gif" width="200" />

**Cost:** Pac-Man finds the food in 10 steps.

**Strategy:** 
DFS prioritises depth over breadth, *i.e.*, it builds Pac-Man's path by exploring a nearby cell, then the cell next to that, then the cell next to that, and so on, down a path as deep as it goes until DFS reaches the goal cell. 

We can see by the red overlay in the animation that DFS traverses the left side of the maze first, then turns east at the first cross-roads. There is no food down this path, so DFS tries again and follows the path down south at the first cross-roads. Since this path leads to food, DFS doesn't bother looking down a different path, and this is the path that Pac-Man takes.

#### Breadth-First Search (BFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=bfs` and get:

<img align="left" src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_bfs.gif" width="200" />

**Cost:** Pac-Man finds a more efficient path in 8 steps.

**Strategy:** Since BFS gives precedence to breadth over depth, the algorithm builds a different path than DFS for Pac-Man: BFS explores all the neighbouring cells 1 step away, and if none are the goal cell, BFS tries the cells 2 steps away, and if it finds no goal cell, BFS tries looking 3 steps away, and so on. In this maze, BFS explores the path down the left side and the path down the right side concurrently, and the right path yields food earlier (in 8 steps rather than 10), so the right path is the one that Pac-Man takes. BFS yields the shortest path to the goal.


