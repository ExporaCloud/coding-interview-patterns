# Two Pointers

## Trigger
The input is sorted (or can be sorted), and you need to find a pair, a triple, or partition the array in place. The brute force checks every pair at O(n^2).

## How it works
Place two pointers and move them based on a comparison, so each step eliminates possibilities without backtracking. Three common shapes:
- **Opposite ends:** left at the start, right at the end, move inward based on whether the current pair is too small or too big.
- **Same direction (fast/slow):** one pointer scans ahead, the other marks a boundary (dedup, partition, cycle detection).
- **Two sequences:** one pointer per array, advance the smaller (the merge step).

## Template (opposite ends)
```
left, right = 0, n - 1
while left < right:
    s = arr[left] + arr[right]
    if s == target: return (left, right)
    if s < target: left += 1
    else: right -= 1
```

## Classic problems
- Two Sum II, Input Array Is Sorted (LC 167)
- 3Sum (LC 15)
- Container With Most Water (LC 11)
- Remove Duplicates from Sorted Array (LC 26, fast/slow)
- Valid Palindrome (LC 125)

## Complexity
Time O(n) after sorting, or O(n log n) including the sort. Space O(1).

## vs Sliding Window
Sliding window keeps a contiguous region and both pointers move the same way. Two pointers often close in from both ends, and the elements between them are not a window you aggregate. If the array must be sorted first, it is almost always two pointers.

## See it run
Watch both pointers move and the search space shrink between them: ▶ https://tryexpora.com/algorithm-debugger
