# Heap / Top K Elements

## Trigger
The question asks for the k largest, smallest, most frequent or closest elements, the kth largest, or a median that changes as data arrives. Sorting everything works at O(n log n), but you only care about k of the n elements.

## How it works
Keep a heap of size k that holds the best k candidates seen so far. For the k *largest*, use a **min**-heap: its top is the weakest of the current top k, so any new element only has to beat that one. Push each element; if the heap grows past k, pop the top. At the end the heap holds the answer, and its top is the kth largest.

For a running median, keep two heaps: a max-heap for the lower half and a min-heap for the upper half, balanced in size.

## Template (k largest)
```
heap = []                          # min-heap
for x in nums:
    heappush(heap, x)
    if len(heap) > k:
        heappop(heap)              # evict the smallest
return heap[0]                     # kth largest
```

## Worked example
**Kth Largest Element in an Array (LC 215)** on `[3, 2, 1, 5, 6, 4]` with `k = 2`.

| x | push | evicted (heap > k) | heap after |
|:---:|:---:|:---:|:---:|
| 3 | 3 | | `3` |
| 2 | 2 | | `2 3` |
| 1 | 1 | 1 | `2 3` |
| 5 | 5 | 2 | `3 5` |
| 6 | 6 | 3 | `5 6` |
| 4 | 4 | 4 | `5 6` |

Answer: **5**, the top of the min-heap. The heap never holds more than 3 elements, which is why the cost is O(n log k) instead of O(n log n).

## Classic problems
- Kth Largest Element in an Array (LC 215)
- Top K Frequent Elements (LC 347)
- K Closest Points to Origin (LC 973)
- Merge k Sorted Lists (LC 23)
- Find Median from Data Stream (LC 295)

## Complexity
Time O(n log k): n pushes and pops on a heap of size k. Space O(k).

## Common mistakes
- **Using a max-heap for the k largest.** You then have to keep all n elements. A min-heap of size k is the trick.
- **Python's `heapq` is a min-heap only.** For a max-heap, push negated values, and negate again when you read them.
- **Top K Frequent without counting first.** Build the frequency map, then heap the `(count, value)` pairs.
- **Two-heap median drifting out of balance.** After each insert, move one element across so the sizes differ by at most one.

## vs Sorting and Quickselect
Sorting is simpler and fine when k is close to n. Quickselect finds the kth element in O(n) on average but O(n^2) in the worst case, and it needs the whole array up front. A heap is the only one of the three that works on a stream.

## See it run
Watch the heap admit, reorder and evict values while the top k settle in: ▶ https://tryexpora.com/algorithm-debugger
