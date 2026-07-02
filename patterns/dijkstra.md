# Dijkstra's Algorithm

## Trigger
Shortest path in a weighted graph with non-negative edge weights. BFS is not enough because edges cost different amounts; you cannot count steps, you must sum weights.

## How it works
Greedily expand the closest unvisited node. A min-heap keyed by distance always hands you the nearest frontier node. When you pop a node, its shortest distance is final. Relax each neighbor: if going through the current node is cheaper, update the neighbor's distance and push it. Non-negative weights are what make "the popped node is final" true; negative edges break that, so use Bellman-Ford there.

## Template
```
dist = {start: 0}
heap = [(0, start)]
while heap:
    d, node = heappop(heap)
    if d > dist[node]: continue          # stale entry
    for nxt, w in neighbors(node):
        nd = d + w
        if nd < dist.get(nxt, inf):
            dist[nxt] = nd
            heappush(heap, (nd, nxt))
```

## Classic problems
- Network Delay Time (LC 743)
- Cheapest Flights Within K Stops (LC 787, Dijkstra variant)
- Path With Minimum Effort (LC 1631)
- Swim in Rising Water (LC 778)

## Complexity
Time O((V + E) log V) with a binary heap. Space O(V).

## vs BFS
Use BFS when every edge costs the same (it is Dijkstra with all weights equal to 1). Reach for Dijkstra the moment weights differ. If weights can be negative, neither works; use Bellman-Ford.

## See it run
Watch the heap hand you the nearest node and the distances relax one edge at a time: ▶ https://tryexpora.com/algorithm-debugger
