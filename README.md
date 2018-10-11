# Pac-Man
A Python implementation of artificial intelligence search algorithms to solve problems within the Berkeley Pac-Man environment. The [Pac-Man Projects, developed at UC Berkeley](http://ai.berkeley.edu), apply AI concepts to the classic arcade game. I help Pac-Man find food, avoid ghosts, and maximise his game score using uninformed and informed state-space search, probabilistic inference, and reinforcement learning.

This project uses Python 2.7.13 plus NumPy 1.13.1 and SciPy 0.19.1.

## Table of Contents
* [How to Play](https://github.com/thiadeliria/Pacman#how-to-play)
* [Uninformed Search](https://github.com/thiadeliria/Pacman#uninformed-search)
    * [Small Search Space](https://github.com/thiadeliria/Pacman#depth-first-search-vs-breadth-first-search-small-search-space)
        * [Depth-First Search](https://github.com/thiadeliria/Pacman#depth-first-search-dfs)
        * [Breadth-First Search](https://github.com/thiadeliria/Pacman#breadth-first-search-bfs)
        * [Comparison]()
    * [Large Search Space](https://github.com/thiadeliria/Pacman#depth-first-search-vs-breadth-first-search-large-search-space)
        * [Depth-First Search](https://github.com/thiadeliria/Pacman#depth-first-search-dfs-1)
        * [Breadth-First Search](https://github.com/thiadeliria/Pacman#breadth-first-search-bfs-1)
        * [Comparison]()


## How to Play
Use WASD or arrow keys to control Pac-Man. To start an interactive game, type at the command line:

`python pacman.py`

<p align="center">
<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/interactive.gif" width="540" />
</p>

To see how Pac-Man fares using search algorithms, we can define some variables:

`python pacman.py -l MAZE_TYPE -p SearchAgent -a fn=SEARCH_ALGO` where `MAZE_TYPE` defines the map layout, and `SearchAgent` navigates Pac-Man through the maze according to the algorithm supplied in the `SEARCH_ALGO` parameter.


## Uninformed Search
Given the inputs:
* initial state - the maze cell that Pac-Man starts in,
* successor function - possible actions that he can take (*e.g.*, *move East*), and
* goal state - the cell that he wants to be in,

the search algorithm returns a sequence of states that leads Pac-Man from initial to goal state. The strategy is to iteratively generate a list of successor states (called the *frontier*) until a path to the goal state is found.

### Depth-First Search vs. Breadth-First Search (small search space)
We can compare some algorithms by observing how Pac-Man fares on a tinyMaze `MAZE_TYPE` with a fixed food dot.

<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/tinymaze.png" width="200" title="tinyMaze"/>
</p>

Pac-Man's initial state is in the upper right corner of the maze. His goal state is a cell containing food, which in this case is the cell in the lower left corner.

#### Depth-First Search (DFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=dfs` and get:
<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/tiny_dfs.gif" width="200" title="DFS on tinyMaze"/>
</p>

**Cost:** Pac-Man finds the food in 10 steps.

**Search nodes expanded:** DFS explores 15 cells in the process of finding a solution.

<img align="left" src="https://github.com/thiadeliria/Pacman/blob/master/gifs/tiny_dfs_paths.png" width="200" title="DFS paths on tinyMaze"/>

**Strategy:** The frontier that DFS constructs is a LIFO (last-in, first-out) stack. The algorithm adds a successor to the frontier and immediately expands it; in other words, it builds a path by exploring a neighbouring cell, then exploring the cell next to that, then the cell next to that, and so on. For instance, it determines Pac-Man can go either west or south from the initial state, but chooses to explore the path heading west to the end before considering the path heading south.

The path that DFS explores first is indicated in white. At the end of this path, DFS has no new un-explored cells, and has found no food. Therefore DFS moves to the next un-explored state on the frontier: it "backtracks" to the last cross-roads and continues down the green path. DFS finds food and reaches a goal state, so it doesn't bother looking down a different path, and this is the path that Pac-Man takes.

#### Breadth-First Search (BFS)
We do `python pacman.py -l tinyMaze -p SearchAgent -a fn=bfs` and get:
<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/tiny_bfs.gif" width="200" title="BFS on tinyMaze"/>
</p>

**Cost:** Pac-Man finds a more efficient path in 8 steps.

**Search nodes expanded:** 15.

<img align="left" src="https://github.com/thiadeliria/Pacman/blob/master/gifs/tiny_bfs_paths.gif" width="200" title="BFS paths on tinyMaze"/>

**Strategy:** BFS builds the frontier in a different strategy. It is a FIFO (first-in, first-out) queue and expands successors in the order they were added. Consider the animation on the left. At the initial state, BFS explores the path heading west and the path heading south concurrently. BFS explores all the neighbouring cells on each path that are 1 step away. Since none are the goal cell, BFS tries the cells 2 steps away, and again it finds no goal cell, so BFS tries looking 3 steps away, and so on. 

By the 8th iteration, BFS finds that the path heading south yields food, so that is the path that Pac-Man takes.

#### Comparison
On a tinyMaze, BFS has an advantage. The order in which it builds the frontier ensures that all shorter paths are expanded prior to any longer path. BFS guarantees the shortest solution (= optimality).

### Depth-First Search vs. Breadth-First Search (large search space)
Let's compare the two algorithms on a `MAZE_TYPE` with a greater search space. The mediumMaze has in total 269 cells or search nodes, compared to tinyMaze's 15.

<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/mediummaze.png" title="mediumMaze"/>
</p>

Pac-Man's initial state is the cell in the upper right corner. His goal state is a cell containing food, which is the cell in the lower left corner.

#### Depth-First Search (DFS)
We try `python pacman.py -l mediumMaze -p SearchAgent -a fn=dfs`.
<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/medium_dfs.gif" title="DFS on mediumMaze"/>
</p>
<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/medium_dfs_text.png" title="DFS on tinyMaze, text"/>

**Cost:** Pac-Man finds the food in 130 steps.

**Search nodes expanded:** 146.

#### Breadth-First Search (BFS)
We do `python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs` and get:
<p align="center">
 <img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/medium_bfs.gif" title="BFS on mediumMaze"/>
</p>
<img src="https://github.com/thiadeliria/Pacman/blob/master/gifs/medium_bfs_text.png" title="BFS on tinyMaze, text"/>

**Cost:** Pac-Man finds the food in 68 steps.

**Search nodes expanded:** 269.

### Comparison
Again, BFS beats DFS by a shorter path. The BFS solution is optimal - but notice the difference in 'Search nodes expanded' - 146 nodes versus 269. BFS finds the shortest-length solution, but sacrifices space as it expands every node in the search space. The more successors each state has (= the higher the branching factor), the more storage BFS uses. The advantage of DFS, low space complexity, is visible in cases with a high branching factor.
