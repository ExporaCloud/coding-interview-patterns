# Prefix Sum

## Trigger
You answer many range-sum queries on the same array, or you count subarrays whose sum equals a target. The brute force recomputes each sum from scratch at O(n) per query, or O(n^2) over all subarrays.

## How it works
`prefix[i]` is the sum of the first `i` elements. The sum of any range `[l, r]` is then `prefix[r + 1] - prefix[l]`, one subtraction. For counting subarrays, flip the question: a subarray ending here sums to `k` exactly when some earlier prefix equals `current - k`. Keep a hash map of how many times each prefix has appeared and you count them in one pass.

Seed the map with `{0: 1}`: the empty prefix, so subarrays that start at index 0 are counted.

## Template (count subarrays with sum k)
```
count = 0
running = 0
seen = {0: 1}                     # prefix sum -> times seen
for x in nums:
    running += x
    count += seen.get(running - k, 0)
    seen[running] = seen.get(running, 0) + 1
```

## Worked example
**Subarray Sum Equals K (LC 560)** on `[3, 4, 7, 2, -3, 1, 4, 2]` with `k = 7`.

| x | running sum | look for (sum - 7) | times seen | count |
|:---:|:---:|:---:|:---:|:---:|
| 3 | 3 | -4 | 0 | 0 |
| 4 | 7 | 0 | 1 | **1** |
| 7 | 14 | 7 | 1 | **2** |
| 2 | 16 | 9 | 0 | 2 |
| -3 | 13 | 6 | 0 | 2 |
| 1 | 14 | 7 | 1 | **3** |
| 4 | 18 | 11 | 0 | 3 |
| 2 | 20 | 13 | 1 | **4** |

Answer: **4** subarrays: `[3,4]`, `[7]`, `[7,2,-3,1]` and `[1,4,2]`. Each one is found the moment its last element arrives, by looking up the prefix that came just before it.

## Classic problems
- Range Sum Query - Immutable (LC 303)
- Subarray Sum Equals K (LC 560)
- Product of Array Except Self (LC 238, prefix products)
- Continuous Subarray Sum (LC 523)
- Range Sum Query 2D - Immutable (LC 304)

## Complexity
Building the prefix array is O(n) time and O(n) space; each range query is then O(1). Counting subarrays with the hash map is O(n) time and O(n) space.

## Common mistakes
- **Forgetting the `{0: 1}` seed.** Subarrays that start at index 0 are never counted.
- **Updating the map before the lookup.** With `k = 0` you would count the empty subarray. Look up first, then record.
- **Off-by-one in the range formula.** With `prefix[0] = 0`, the sum of `[l, r]` is `prefix[r + 1] - prefix[l]`.
- **Reaching for a sliding window with negative numbers.** A window only works when growing it can only increase the sum. With negatives, use prefix sums.

## vs Sliding Window
A [sliding window](sliding-window.md) needs the sum to grow as the window grows, so it breaks on negative numbers. Prefix sums do not care about the sign, which makes them the default for "count subarrays with sum k".

## See it run
Watch the running sum grow and each lookup find the earlier prefix that closes a subarray: ▶ https://tryexpora.com/algorithm-debugger
