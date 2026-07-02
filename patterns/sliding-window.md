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

## Worked example
**Longest Substring Without Repeating Characters (LC 3)** on input `"abcabcbb"`. The window holds the current run of unique characters. When a duplicate arrives, shrink from the left until it is gone.

```
index:  0   1   2   3   4   5   6   7
char:   a   b   c   a   b   c   b   b
```

| right | char | duplicate? | action | window | best |
|:---:|:---:|:---|:---|:---:|:---:|
| 0 | a | no | add a | `a` | 1 |
| 1 | b | no | add b | `ab` | 2 |
| 2 | c | no | add c | `abc` | **3** |
| 3 | a | yes | drop left until a is free, add a | `bca` | 3 |
| 4 | b | yes | drop left until b is free, add b | `cab` | 3 |
| 5 | c | yes | drop left until c is free, add c | `abc` | 3 |
| 6 | b | yes | drop left past a and b, add b | `cb` | 3 |
| 7 | b | yes | drop left until b is free, add b | `b` | 3 |

The window never rescans; `left` only ever moves forward. Answer: **3** (`abc`). That single forward-only sweep is what turns the O(n^2) brute force into O(n).

## Classic problems
- Longest Substring Without Repeating Characters (LC 3)
- Minimum Window Substring (LC 76)
- Longest Repeating Character Replacement (LC 424)
- Fruit Into Baskets (LC 904)
- Maximum Average Subarray I (LC 643, fixed size)

## Complexity
Time O(n). Space O(k) for the window bookkeeping, where k is the number of distinct elements or the charset size.

## Common mistakes
- **Shrinking with `if` instead of `while`.** After a duplicate or a broken constraint you may need to remove several elements, not one. Loop until the window is valid again.
- **Measuring `best` while the window is invalid.** Only record the answer after you have restored the constraint.
- **Off-by-one in the window length.** The size of `[left, right]` is `right - left + 1`, not `right - left`.
- **Fixed-size windows: forgetting to evict.** With a width of K, every element that enters on the right must push one out on the left, or the window silently grows.

## vs Two Pointers
Two pointers often move toward each other from both ends of sorted data. A sliding window is two pointers moving the same direction, both left to right, maintaining a contiguous region you aggregate over. If the region must stay contiguous and you track something inside it, it is a window.

## See it run
Watch the window expand and shrink at every step, with the counts inside it updating live: ▶ https://tryexpora.com/algorithm-debugger
