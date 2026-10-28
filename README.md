# LeetCode Patterns: The 15 Coding Interview Patterns, Visually

![License](https://img.shields.io/badge/license-MIT-blue) ![Made by Expora](https://img.shields.io/badge/made%20by-Expora-6d28d9) ![Patterns](https://img.shields.io/badge/patterns-15-informational)

> Most coding interview problems are variations of a small set of patterns. Learn to recognize the **structural signal** that triggers each one, and you stop memorizing 500 problems and start solving the ones you have never seen.

This is an open guide to the **15 LeetCode patterns behind most coding interview problems**: the trigger that fires each one, a template, a worked step-by-step trace, the classic problems, the complexity, and the mistakes that cost people the interview. Everything here is free markdown, MIT licensed, and reads on its own.

Want them on one page? The [LeetCode patterns cheat sheet](https://tryexpora.com/coding-interview-patterns) puts all 15 signals side by side.

---

## The core 7

Start here. These cover the bulk of medium problems.

| Pattern | Trigger (structural signal) | Classic problems | Doc |
|---|---|---|---|
| **Sliding Window** | Contiguous subarray/substring + "longest/shortest/at most K" | Longest Substring Without Repeat (LC 3), Min Window Substring (LC 76) | [→](patterns/sliding-window.md) |
| **Two Pointers** | Sorted input, or pairs from both ends, or in-place partition | Two Sum II (LC 167), 3Sum (LC 15), Container With Most Water (LC 11) | [→](patterns/two-pointers.md) |
| **Binary Search** | Sorted array, or a monotonic answer space ("minimum X that works") | Search Insert (LC 35), Koko Eating Bananas (LC 875) | [→](patterns/binary-search.md) |
| **BFS** | Shortest path in unweighted graph/grid, or level-order | Number of Islands (LC 200), Rotting Oranges (LC 994) | [→](patterns/bfs.md) |
| **DFS** | Visit everything reachable: components, paths, cycle detection | Number of Islands (LC 200), Clone Graph (LC 133) | [→](patterns/dfs.md) |
| **Dynamic Programming** | Overlapping subproblems + optimal substructure ("count ways", "min cost") | Climbing Stairs (LC 70), Coin Change (LC 322), House Robber (LC 198) | [→](patterns/dynamic-programming.md) |
| **Dijkstra** | Shortest path in a weighted graph, non-negative weights | Network Delay Time (LC 743), Cheapest Flights (LC 787) | [→](patterns/dijkstra.md) |

## 8 more patterns

Each one owns a specific family of problems. When a problem resists the core 7, it is usually one of these.

| Pattern | Trigger (structural signal) | Classic problems | Doc |
|---|---|---|---|
| **Backtracking** | Generate all subsets, permutations or combinations; choose, explore, undo | Subsets (LC 78), Permutations (LC 46), N-Queens (LC 51) | [→](patterns/backtracking.md) |
| **Monotonic Stack** | Next greater or smaller element, spans bounded by the nearest taller bar | Daily Temperatures (LC 739), Largest Rectangle in Histogram (LC 84) | [→](patterns/monotonic-stack.md) |
| **Fast & Slow Pointers** | Cycle or middle node in a linked list or sequence, O(1) space | Linked List Cycle (LC 141), Find the Duplicate Number (LC 287) | [→](patterns/fast-slow-pointers.md) |
| **Prefix Sum** | Repeated range sums, or count subarrays that sum to K | Subarray Sum Equals K (LC 560), Range Sum Query (LC 303) | [→](patterns/prefix-sum.md) |
| **Heap / Top K** | k largest, kth largest, k most frequent, running median | Kth Largest Element (LC 215), Top K Frequent Elements (LC 347) | [→](patterns/heap-top-k.md) |
| **Merge Intervals** | Ranges that may overlap: merge, insert, count active at once | Merge Intervals (LC 56), Meeting Rooms II (LC 253) | [→](patterns/merge-intervals.md) |
| **In-place Linked List Reversal** | Reverse a list, or part of it, without new nodes | Reverse Linked List (LC 206), Reverse Nodes in k-Group (LC 25) | [→](patterns/linked-list-reversal.md) |
| **Topological Sort** | Tasks with dependencies: find a valid order or prove a cycle | Course Schedule (LC 207), Alien Dictionary (LC 269) | [→](patterns/topological-sort.md) |

**More:**
- [Decision framework](decision-framework.md) — the questions to ask an unfamiliar problem to find its pattern
- [Combining patterns](combining-patterns.md) — how the hard problems stack two patterns together
- [Complexity cheatsheet](complexity-cheatsheet.md) — time and space by pattern

---

## Why pattern recognition

Reading a finished solution tells you *what* the code does. It does not show you *how* the algorithm moves. You see the two pointers in the final code, but not the moment the right pointer stops and the left one starts catching up. You see the DP array, but not the order the cells fill in.

That gap, between reading code and understanding execution, is why 150 solved problems still end in a freeze during the interview. You memorized outcomes, not mechanics.

The way to close it is to learn each pattern by its structural trigger and trace it step by step until the mechanic is obvious. That is what makes a pattern *recognizable* the next time, on a problem you have never seen. Each doc here walks one pattern through a worked trace with exactly that goal.

---

## How to use this repo

1. Start with the [decision framework](decision-framework.md) — learn to read a problem for its trigger before you touch code.
2. Work through the core 7, then the 8 more. For each, read the trigger, then follow the worked example until the mechanic is clear.
3. Use the [complexity cheatsheet](complexity-cheatsheet.md) to sanity-check your solutions.
4. When problems start feeling like combinations, read [combining patterns](combining-patterns.md).

The goal is not to finish this repo. It is to reach the point where a new problem announces its own pattern.

---

Built by the team behind [Expora](https://tryexpora.com), a visual algorithm debugger for coding interviews (early access).
