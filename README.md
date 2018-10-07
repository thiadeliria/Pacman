## Overview
**Summary:** a Python implementation of AI search algorithms to solve problems within the Berkeley Pac-Man environment. The Pac-Man Projects, developed at [UC Berkeley](http://ai.berkeley.edu), apply AI concepts to the classic arcade game Pac-Man.

**Dependencies:** Python 2.7

**Concepts:** informed state-space search, probabilistic inference, reinforcement learning.

## How to Play
Use WASD or arrow keys to control Pac-Man. To start an interactive game, type at the command line:

`python pacman.py`

<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_default.gif" width="540" />


Variables can be defined as follows:

`python pacman.py -l MAZE_TYPE -p SearchAgent -a fn=SEARCH_ALGO` where `MAZE_TYPE` defines the map layout, and `SearchAgent` navigates Pac-Man through the maze according to the algorithm supplied in the `SEARCH_ALGO` parameter.


## Search Algorithms
Search algorithms guide Pac-Man on his dot-gobbling, ghost-avoiding adventure. We compare how Pac-Man fares with each algorithm on a tinyMaze `MAZE_TYPE` with a fixed food dot.

The algorithm determines the path that Pac-Man takes to get to the goal cell (in this case, the cell containing food) from the start cell (his position in the upper right corner). Specifically, it views the maze as a graph in which each cell on the maze grid constitutes a node. The algorithm makes a queue of un-explored cells for Pac-Man to visit in order. The cells that Pac-Man explores first are coloured a deeper red.

#### Depth-First Search (DFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs` and get:

<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_dfs.gif" width="200" /> <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_dfs_text.png" />

Pac-Man takes a cost of 10 steps to find the food dot. The DFS algorithm prioritises depth over breadth, i.e., it builds Pac-Man's path by exploring a nearby cell, then the cell next to that, then the cell next to that, and so on, down a path as deep as it goes until DFS reaches the goal cell. We can see by the red overlay in the animation that DFS traverses the left side of the maze first, then turns east at the first cross-roads. There is no food down this path, so DFS tries again and follows the path down south at the first cross-roads. Since this path leads to food, DFS doesn't bother looking down a different path, and this is the path that Pac-Man takes.

#### Breadth-First Search (BFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=bfs` and get:

<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_bfs.gif" width="200" /> <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/pacman_bfs_text.png" />

We see that Pac-Man doing BFS takes a smaller cost (8) to find the same food dot. Since BFS gives precedence to breadth over depth, the algorithm builds a different path than DFS for Pac-Man: BFS explores all the neighbouring cells 1 step away, and if none are the goal cell, BFS puts all cells 2 steps away onto the queue, and if those aren't the goal, BFS tries looking 3 steps away, and so on. In this maze, BFS explores the path down the left side and the path down the right side concurrently, and the right path yields food earlier (in 8 steps rather than 10), so the right path is the one that Pac-Man takes.

#### Uniform-Cost Search (UCS)

#### A* Search
