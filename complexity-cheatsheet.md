# Complexity Cheatsheet

Time and space for each pattern, with the reason behind the number. n is the input size unless stated.

| Pattern | Time | Space | Why |
|---|---|---|---|
| Sliding Window | O(n) | O(k) | Each element enters and leaves the window once; k = distinct elements tracked |
| Two Pointers | O(n) | O(1) | Both pointers traverse the array once, no extra structure |
| Binary Search | O(log n) | O(1) | Halves the search space each step |
| BFS | O(V + E) | O(V) | Visits every vertex and edge once; queue holds up to a level |
| DFS / Backtracking | O(branches^depth) | O(depth) | Explores the decision tree; space is the recursion stack |
| Dijkstra | O((V + E) log V) | O(V) | Each edge relax may push to the heap; heap ops are log V |
| Dynamic Programming | O(states x transition) | O(states) | One computation per state, reused; space often reduces to one row |

## Notes that cost people points
- **Binary Search on the answer** is O(log(range) x check), not O(log n). The check is often O(n), so the total is O(n log(range)).
- **Backtracking** is exponential by nature. Pruning does not change the worst case but changes the practical runtime enormously (N-Queens is unsolvable at n=12 without pruning, instant with it).
- **DP space reduction:** if state t only depends on t-1, you do not need the full table, just two rows (or one). Interviewers love this follow-up.
- **Dijkstra with a plain array** instead of a heap is O(V^2), which is faster for dense graphs where E is close to V^2.

## See it run
Watching the state count grow is the clearest way to feel a complexity. ▶ https://tryexpora.com/algorithm-debugger
