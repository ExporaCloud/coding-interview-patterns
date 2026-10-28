# The Decision Framework

You do not need to recognize the answer. You need to recognize the pattern. These are the questions to ask an unfamiliar problem, in order, before you write any code.

## 1. What is the shape of the input?
- **Sorted array?** Think Binary Search or Two Pointers.
- **Contiguous subarray or substring?** Think Sliding Window.
- **Tree or graph?** Think BFS or DFS.
- **Directed graph of dependencies?** Think Topological Sort.
- **Linked list?** Think Fast & Slow Pointers or In-place Reversal.
- **List of ranges?** Think Merge Intervals.
- **Weighted graph, shortest path?** Think Dijkstra.
- **"Count the ways" or "min/max cost" over choices?** Think Dynamic Programming.

## 2. What is the question asking?
- **Shortest path, fewest steps, unweighted?** BFS.
- **Visit everything reachable, or does a path exist?** DFS.
- **All combinations, permutations or subsets?** Backtracking.
- **Next greater or smaller element?** Monotonic Stack.
- **Top k, kth largest, running median?** Heap.
- **Count subarrays that sum to K?** Prefix Sum.
- **Longest or shortest window under a constraint?** Sliding Window.
- **A single optimal value built from smaller optimal values?** DP.

## 3. What is the brute force, and what is wasteful about it?
The pattern is usually the fix for a specific waste:
- Recomputing overlapping subproblems, use DP (memoize them).
- Re-scanning the same subarray, use Sliding Window (reuse the window).
- Scanning a sorted space linearly, use Binary Search (halve it).
- Checking every pair, use Two Pointers (move inward).
- Looking ahead from every element, use a Monotonic Stack (resolve many at once).
- Re-adding the same range again and again, use Prefix Sum (subtract two prefixes).
- Sorting everything to keep k of it, use a Heap of size k.

## 4. Is the answer space monotonic?
If "X works implies X+1 works" (or the reverse), you can binary search the answer even when the input is not a sorted array. This is how Koko Eating Bananas (LC 875) and Split Array Largest Sum (LC 410) become binary search.

## The 15 triggers at a glance
| If you see... | Reach for |
|---|---|
| Sorted array, find a pair or a target | Two Pointers / Binary Search |
| Contiguous window + "at most / longest / shortest" | Sliding Window |
| Unweighted shortest path or level order | BFS |
| Visit everything reachable, components, cycles | DFS |
| All subsets, all permutations, all combinations | Backtracking |
| Weighted shortest path, non-negative | Dijkstra |
| Overlapping subproblems + optimal substructure | Dynamic Programming |
| Next greater / smaller element | Monotonic Stack |
| Cycle or middle of a linked list | Fast & Slow Pointers |
| Range sums, subarrays summing to K | Prefix Sum |
| k largest / most frequent, running median | Heap / Top K |
| Overlapping ranges | Merge Intervals |
| Reverse a list or part of it in place | In-place Linked List Reversal |
| Dependencies, valid order, cycle check | Topological Sort |

## How the patterns relate
Several patterns are the same idea with one thing added. Seeing the links makes them easier to recall and to tell apart:

```mermaid
graph LR
    Sorted["Sorted array"] --> BS["Binary Search"]
    Sorted --> TP["Two Pointers"]
    TP -->|"same direction, contiguous region"| SW["Sliding Window"]
    BFS["BFS"] -->|"add edge weights"| DJ["Dijkstra"]
    DFS["DFS"] -->|"undo on the way back"| BT["Backtracking"]
    BT -->|"add memoization"| DP["Dynamic Programming"]
    BFS -->|"wait for in-degree 0"| TS["Topological Sort"]
    TP -->|"same direction, different speeds"| FS["Fast & Slow Pointers"]
```

- **BFS is Dijkstra with every weight equal to 1.** The moment edges cost different amounts, BFS breaks and you need the heap.
- **Backtracking is DFS that undoes its choices, and backtracking plus memoization is top-down DP.** If the same subproblem repeats across branches, cache it and the exponential search collapses.
- **Sliding Window is Two Pointers moving the same direction** over a contiguous region you aggregate, rather than closing in from both ends.

## See it run
The fastest way to internalize a trigger is to watch the pattern execute once. ▶ https://tryexpora.com/algorithm-debugger
