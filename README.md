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
Search algorithms guide Pac-Man on his dot-gobbling, ghost-avoiding adventure. Specifically, they determine the path that Pac-Man follows.

#### Depth-First Search (DFS)

#### Breadth-First Search (BFS)

#### Uniform-Cost Search (UCS)

#### A* Search
