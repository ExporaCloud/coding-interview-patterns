# DFS

## Trigger
You need to visit everything reachable in a tree, graph or grid: count connected components, find root-to-leaf paths, detect a cycle, or check whether two nodes connect. The question is about *reaching* or *covering*, not about the shortest route.

## How it works
Depth-first search goes as deep as it can along one branch before it backs up and tries the next. A `visited` set (or marking the grid in place) guarantees each node is processed once. Recursion gives you the stack for free; an explicit stack does the same thing without the recursion limit.

## Template (grid, recursive)
```
def dfs(r, c):
    if out_of_bounds(r, c) or grid[r][c] != LAND:
        return
    grid[r][c] = VISITED              # mark before recursing
    for dr, dc in [(1,0), (-1,0), (0,1), (0,-1)]:
        dfs(r + dr, c + dc)

for each cell (r, c):
    if grid[r][c] == LAND:
        count += 1
        dfs(r, c)                     # sinks the whole island
```

## Worked example
**Number of Islands (LC 200)** on this grid. The outer loop scans row by row; every time it lands on unvisited land, that is a new island, and DFS sinks all of it.

```
      c0  c1  c2  c3
r0:   1   1   0   0
r1:   1   0   0   1
r2:   0   0   1   1
```

| scan reaches | value | action | cells sunk by DFS | islands |
|:---:|:---:|:---|:---|:---:|
| (0,0) | 1 | new island, start DFS | (0,0), (0,1), (1,0) | **1** |
| (0,1) | sunk | skip | | 1 |
| (1,0) | sunk | skip | | 1 |
| (1,3) | 1 | new island, start DFS | (1,3), (2,3), (2,2) | **2** |
| (2,2) | sunk | skip | | 2 |
| (2,3) | sunk | skip | | 2 |

Answer: **2**. Every cell is touched a constant number of times, once by the scan and at most once by a DFS, so the whole thing is O(rows x cols).

## Classic problems
- Number of Islands (LC 200)
- Maximum Depth of Binary Tree (LC 104)
- Clone Graph (LC 133)
- Path Sum (LC 112)
- Pacific Atlantic Water Flow (LC 417)

## Complexity
Time O(V + E), or O(rows x cols) on a grid. Space O(V) for the visited set plus the recursion stack, which can reach O(V) on a long path.

## Common mistakes
- **Marking visited after the recursive calls.** Neighbours then loop back into the same cell. Mark it before you recurse.
- **Recursion depth on big grids.** A 1000 x 1000 grid of land can overflow the default stack. Switch to an explicit stack.
- **Forgetting the bounds check comes first.** Read `grid[r][c]` only after you know `r` and `c` are inside.
- **Cycle detection in directed graphs with one set.** You need two states: "on the current path" and "fully done". A single `visited` set flags false cycles.

## vs BFS and Backtracking
[BFS](bfs.md) explores ring by ring, so the first time it reaches a node is along the shortest path. DFS gives no such guarantee, so use it when any path or full coverage is enough. [Backtracking](backtracking.md) is DFS over choices that un-marks on the way back, because one element can belong to many answers.

## See it run
Watch the recursion dive, hit a wall and back up, with every visited cell marked live: ▶ https://tryexpora.com/algorithm-debugger

Go deeper: [BFS, DFS or Dijkstra? How to pick in an interview](https://tryexpora.com/blog/graph-algorithms-coding-interview)
