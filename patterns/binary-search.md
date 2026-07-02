# Binary Search

## Trigger
A sorted array, or a monotonic answer space where "if X works, everything above X works" (or below). The brute force scans linearly at O(n).

## How it works
Maintain a range `[lo, hi]` that must contain the answer. Check the middle. Discard the half that cannot contain the answer. Repeat until the range collapses. The subtle part is the invariant: be precise about what "the answer is in [lo, hi]" means, so the boundary updates are correct and the loop terminates.

## Template
```
lo, hi = 0, n - 1
while lo <= hi:
    mid = lo + (hi - lo) // 2
    if arr[mid] == target: return mid
    if arr[mid] < target: lo = mid + 1
    else: hi = mid - 1
return -1
```

## Binary search on the answer
When the input is not sorted but the answer is monotonic, search the answer itself:
```
lo, hi = min_possible, max_possible
while lo < hi:
    mid = lo + (hi - lo) // 2
    if feasible(mid): hi = mid
    else: lo = mid + 1
return lo
```

## Classic problems
- Search Insert Position (LC 35)
- Find First and Last Position (LC 34)
- Koko Eating Bananas (LC 875, on the answer)
- Split Array Largest Sum (LC 410, on the answer)
- Find Minimum in Rotated Sorted Array (LC 153)

## Complexity
Time O(log n) for a sorted array; O(n log(range)) when the feasibility check is O(n). Space O(1).

## vs the rest
If the data is sorted and you want one element, it is binary search, not two pointers. The tell for "binary search on the answer" is a question like "minimum capacity, speed, or size such that something is possible".

## See it run
Watch the range halve and the invariant hold at each step: ▶ https://tryexpora.com/algorithm-debugger
