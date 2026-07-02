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

## Worked example
**Container With Most Water (LC 11)** on heights `[1, 8, 6, 2, 5]`. Two lines form a container and the area is `min(height[left], height[right]) x (right - left)`. Once the pointers close in the width only shrinks, so at each step you move the **shorter** line inward, hoping a taller one lifts the limit.

```
index:   0   1   2   3   4
height:  1   8   6   2   5
```

| left | right | area = min(h) x width | move | best |
|:---:|:---:|:---|:---|:---:|
| 0 (1) | 4 (5) | min(1,5) x 4 = 4 | left is shorter, left++ | 4 |
| 1 (8) | 4 (5) | min(8,5) x 3 = 15 | right is shorter, right-- | **15** |
| 1 (8) | 3 (2) | min(8,2) x 2 = 4 | right is shorter, right-- | 15 |
| 1 (8) | 2 (6) | min(8,6) x 1 = 6 | right is shorter, right-- | 15 |

Pointers meet, stop. Answer: **15**. Moving the taller line could never help, because the shorter line caps the area. That insight is what makes a single O(n) pass correct instead of checking all pairs.

## Classic problems
- Two Sum II, Input Array Is Sorted (LC 167)
- 3Sum (LC 15)
- Container With Most Water (LC 11)
- Remove Duplicates from Sorted Array (LC 26, fast/slow)
- Valid Palindrome (LC 125)

## Complexity
Time O(n) after sorting, or O(n log n) including the sort. Space O(1).

## Common mistakes
- **Moving the wrong pointer.** In Container With Most Water you must move the shorter line; moving the taller one can skip the real answer.
- **Forgetting the input must be sorted** for the two-sum flavour. Moving inward only works because sorted order tells you which side is too small.
- **A pointer that fails to advance** on some branch, causing an infinite loop. Every path through the loop must move `left` or `right`.

## vs Sliding Window
Sliding window keeps a contiguous region and both pointers move the same way. Two pointers often close in from both ends, and the elements between them are not a window you aggregate. If the array must be sorted first, it is almost always two pointers.

## See it run
Watch both pointers move and the search space shrink between them: ▶ https://tryexpora.com/algorithm-debugger
