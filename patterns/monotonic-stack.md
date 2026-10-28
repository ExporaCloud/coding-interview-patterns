# Monotonic Stack

## Trigger
For each element you need the *next* (or previous) greater or smaller element, or a span or area bounded by the nearest taller or shorter bar. The brute force looks ahead from every element at O(n^2).

## How it works
Keep a stack whose values stay in sorted order (for "next greater", decreasing from bottom to top). When a new element arrives that breaks the order, it is the answer for every element it pops. Elements still waiting on the stack have not found their answer yet. Each element is pushed once and popped once, so the scan is O(n).

Store **indices**, not values: you usually need the distance, and you can always read the value back from the array.

## Template (next greater element)
```
answer = [default] * n
stack = []                         # indices, values decreasing
for i in range(n):
    while stack and arr[stack[-1]] < arr[i]:
        j = stack.pop()
        answer[j] = i - j          # or arr[i], depending on the question
    stack.append(i)
```

## Worked example
**Daily Temperatures (LC 739)** on `[73, 74, 75, 71, 69, 72, 76, 73]`. For each day, how many days until a warmer one? The stack holds the days still waiting for a warmer day.

| i | temp | popped (answer set) | stack after (temps) |
|:---:|:---:|:---|:---:|
| 0 | 73 | | `73` |
| 1 | 74 | 73 → 1 | `74` |
| 2 | 75 | 74 → 1 | `75` |
| 3 | 71 | | `75 71` |
| 4 | 69 | | `75 71 69` |
| 5 | 72 | 69 → 1, 71 → 2 | `75 72` |
| 6 | 76 | 72 → 1, 75 → **4** | `76` |
| 7 | 73 | | `76 73` |

Answer: `[1, 1, 4, 2, 1, 1, 0, 0]`. Day 2 (75) waits on the stack for four days until 76 pops it. The two days left at the end never see a warmer day, so they keep the default 0.

## Classic problems
- Daily Temperatures (LC 739)
- Next Greater Element I (LC 496)
- Next Greater Element II (LC 503, circular)
- Largest Rectangle in Histogram (LC 84)
- Trapping Rain Water (LC 42)

## Complexity
Time O(n), because every index is pushed and popped at most once. Space O(n) for the stack in the worst case (a strictly decreasing input).

## Common mistakes
- **Wrong direction of the stack.** Next *greater* keeps a decreasing stack; next *smaller* keeps an increasing one. Swap the comparison and you get the other problem.
- **Strict vs non-strict comparison.** With duplicates, `<` and `<=` give different answers. Decide what "greater" means before you code.
- **Storing values instead of indices.** You lose the distance and the position you need to write the answer.
- **Forgetting the leftovers.** Elements still on the stack at the end have no answer; make sure the default is right.

## vs Two Pointers
Both are O(n) single passes, but two pointers look at two positions at a time. A monotonic stack remembers *every* unresolved element at once, which is what you need when one new value can answer many old questions.

## See it run
Watch elements pile up on the stack and get popped the moment a bigger value arrives: ▶ https://tryexpora.com/algorithm-debugger

Go deeper: [the monotonic stack pattern, explained](https://tryexpora.com/blog/monotonic-stack-pattern)
