# DFS and Backtracking

## Trigger
You need to explore all paths, generate all subsets, permutations, or combinations, or answer "does any path exist". The signal is "all", "every", or a decision tree where each step chooses and may need to undo.

## How it works
Depth-first search commits to a choice, recurses, and comes back. Backtracking adds the undo: choose, explore, un-choose. That un-choose is the whole trick. It restores the state so the next branch starts clean. Every backtracking problem is the same three lines around a recursive call.

## Template (backtracking)
```
def backtrack(path, choices):
    if is_complete(path):
        results.append(path.copy())
        return
    for choice in choices:
        path.append(choice)                     # choose
        backtrack(path, next_choices(choice))   # explore
        path.pop()                              # un-choose
```

## Pruning
N-Queens is Subsets with one extra line: before recursing, skip any choice that already violates a constraint. Pruning does not change the worst case, but it makes exponential problems tractable in practice.

## Classic problems
- Subsets (LC 78)
- Permutations (LC 46)
- Combination Sum (LC 39)
- N-Queens (LC 51)
- Word Search (LC 79)

## Complexity
Time O(branches^depth), exponential by nature. Space O(depth) for the recursion stack plus the current path.

## vs BFS and DP
Use DFS over BFS when you need all paths or existence, not the shortest one. When the same subproblem repeats across branches, add memoization and DFS becomes top-down dynamic programming.

## See it run
Watch the decision tree grow, the path push and pop, and pruning cut whole branches: ▶ https://tryexpora.com/algorithm-debugger
