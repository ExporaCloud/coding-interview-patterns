# Coding Interview Patterns — A Visual Guide

![License](https://img.shields.io/badge/license-MIT-blue) ![Made by Expora](https://img.shields.io/badge/made%20by-Expora-6d28d9) ![Patterns](https://img.shields.io/badge/patterns-7-informational)

> Most coding interview problems are variations of a small set of patterns. Learn to recognize the **structural signal** that triggers each one, and you stop memorizing 500 problems and start solving the ones you have never seen.

This is an open guide to the **7 patterns that cover roughly 80% of coding interview problems** — the trigger that fires each one, the classic problems, the complexity, and how to tell apart the patterns that look alike.

Each pattern links to a **visual debugger** where you can watch it execute step by step — the sliding window expanding and shrinking, the BFS queue draining level by level, the DP table filling cell by cell.

**▶ See the patterns run step by step at [Expora](https://tryexpora.com)**

---

## The 7 patterns

| Pattern | Trigger (structural signal) | Classic problems | Doc | See it run |
|---|---|---|---|---|
| **Sliding Window** | Contiguous subarray/substring + "longest/shortest/at most K" | Longest Substring Without Repeat (LC 3), Min Window Substring (LC 76) | [→](patterns/sliding-window.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **Two Pointers** | Sorted input, or pairs from both ends, or in-place partition | Two Sum II (LC 167), 3Sum (LC 15), Container With Most Water (LC 11) | [→](patterns/two-pointers.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **Binary Search** | Sorted array, or a monotonic answer space ("minimum X that works") | Search Insert (LC 35), Koko Eating Bananas (LC 875) | [→](patterns/binary-search.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **BFS** | Shortest path in unweighted graph/grid, or level-order | Number of Islands (LC 200), Rotting Oranges (LC 994) | [→](patterns/bfs.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **DFS / Backtracking** | Explore all paths / build all combinations, undo and try again | Subsets (LC 78), Permutations (LC 46), N-Queens (LC 51) | [→](patterns/dfs-backtracking.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **Dijkstra** | Shortest path in a weighted graph, non-negative weights | Network Delay Time (LC 743), Cheapest Flights (LC 787) | [→](patterns/dijkstra.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |
| **Dynamic Programming** | Overlapping subproblems + optimal substructure ("count ways", "min cost") | Climbing Stairs (LC 70), Coin Change (LC 322), House Robber (LC 198) | [→](patterns/dynamic-programming.md) | [▶ Expora](https://tryexpora.com/algorithm-debugger) |

**More:**
- [Decision framework](decision-framework.md) — the questions to ask an unfamiliar problem to find its pattern
- [Combining patterns](combining-patterns.md) — how the hard problems stack two patterns together
- [Complexity cheatsheet](complexity-cheatsheet.md) — time and space by pattern

---

## Why visual learning

Reading a finished solution tells you *what* the code does. It does not show you *how* the algorithm moves. You see the two pointers in the final code, but not the moment the right pointer stops and the left one starts catching up. You see the DP array, but not the order the cells fill in.

That gap — between reading code and understanding execution — is why 150 solved problems still end in a freeze during the interview. You memorized outcomes, not mechanics.

A visual debugger closes the gap. You watch the state change at every step: the window, the queue, the call stack, the table. That is what makes a pattern *recognizable* the next time, on a problem you have never seen.

**▶ Try it: [Expora — the visual algorithm debugger](https://tryexpora.com/algorithm-debugger)**

---

## How to use this repo

1. Start with the [decision framework](decision-framework.md) — learn to read a problem for its trigger before you touch code.
2. Work through the 7 pattern docs. For each, read the trigger, then watch it execute on [Expora](https://tryexpora.com) until the mechanic is obvious.
3. Use the [complexity cheatsheet](complexity-cheatsheet.md) to sanity-check your solutions.
4. When problems start feeling like combinations, read [combining patterns](combining-patterns.md).

The goal is not to finish this repo. It is to reach the point where a new problem announces its own pattern.

---

Built by **[Expora](https://tryexpora.com)** — the visual algorithm debugger for coding interviews. Watch BFS, DFS, Dijkstra, dynamic programming, sliding window and binary search execute step by step.
