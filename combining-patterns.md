# Combining Patterns

The core patterns cover the medium problems. The hard problems combine two of them. Once each pattern is automatic on its own, the difficulty moves to recognizing that a problem needs two layers.

## Common combinations

### Sliding Window + Hash Map
The window tracks a contiguous region; the hash map tracks counts or last-seen indices inside it. Minimum Window Substring (LC 76) is a window whose validity is decided by a character-count map.

### Binary Search + Greedy
Binary search the answer, use a greedy feasibility check to test each candidate. Koko Eating Bananas (LC 875): binary search the eating speed, greedily check if she finishes in time. Split Array Largest Sum (LC 410): binary search the max subarray sum, greedily count the splits.

### Backtracking + Memoization = top-down DP
Backtracking explores all choices; memoization caches the result of each state so you never recompute it. Word Break (LC 139) and many "can you reach" problems are DFS with a memo, which is just DP written recursively.

### BFS + State encoding
The graph node is not a cell but a tuple of (position, state). Shortest Path in a Grid With Obstacles Elimination (LC 1293) is BFS where the node is (row, col, obstacles_left).

### Heap + Traversal
Traverse a structure while a heap keeps the top-K or the next-smallest. Merge K Sorted Lists (LC 23) is a traversal driven by a min-heap of list heads.

### Fast & Slow Pointers + In-place Reversal
Find the middle with fast and slow pointers, reverse the second half in place, then walk both halves together. Palindrome Linked List (LC 234) and Reorder List (LC 143) both work this way in O(1) space.

### Sort + Two Pointers
Sort first to unlock the two-pointer move. 3Sum (LC 15) sorts, then fixes one element and two-pointers the rest.

## How to see the seam
When a single pattern stalls, ask: what am I tracking *inside* the pattern? If the thing you track is itself a structure (a map, a heap, a state), that is the second pattern. Learn to name both layers and hard problems stop feeling random.

## See it run
Expora's visual debugger lets you step through the layered patterns and watch both the outer structure and the inner state change together. ▶ https://tryexpora.com/coding-interview-patterns
