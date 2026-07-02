# Sliding Window

## Trigger
You see a contiguous subarray or substring, and the question asks for the longest, the shortest, or an aggregate under a constraint ("at most K distinct", "sum at least target", "no repeating characters"). The brute force checks every subarray at O(n^2) or worse.

## How it works
Keep a window `[left, right]` over the array. Expand `right` to include new elements. When the window breaks the constraint, shrink from `left` until it is valid again. Every element enters the window once and leaves once, so the whole scan is O(n).

Two flavours:
- **Variable size:** grow right, shrink left when invalid, track the best valid window.
- **Fixed size K:** slide a window of constant width, updating the aggregate as one element enters and one leaves.

## Template (variable size)
```
left = 0
for right in range(n):
    add(arr[right])
    while window_invalid():
        remove(arr[left])
        left += 1
    best = max(best, right - left + 1)
```

## Classic problems
- Longest Substring Without Repeating Characters (LC 3)
- Minimum Window Substring (LC 76)
- Longest Repeating Character Replacement (LC 424)
- Fruit Into Baskets (LC 904)
- Maximum Average Subarray I (LC 643, fixed size)

## Complexity
Time O(n). Space O(k) for the window bookkeeping, where k is the number of distinct elements or the charset size.

## vs Two Pointers
Two pointers often move toward each other from both ends of sorted data. A sliding window is two pointers moving the same direction, both left to right, maintaining a contiguous region you aggregate over. If the region must stay contiguous and you track something inside it, it is a window.

## See it run
Watch the window expand and shrink at every step, with the counts inside it updating live: ▶ https://tryexpora.com/algorithm-debugger
