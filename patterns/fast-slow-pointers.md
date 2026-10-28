# Fast & Slow Pointers

## Trigger
A linked list or a sequence where each value points to the next one, and you need to detect a cycle, find the middle node, or find where a loop starts. Usually with an O(1) extra space requirement, which rules out a hash set of visited nodes.

## How it works
Move two pointers through the same sequence at different speeds: `slow` one step at a time, `fast` two steps. If there is no cycle, `fast` falls off the end. If there is one, `fast` enters it first and closes the gap by one node per step until it lands on `slow`. They must meet, they cannot jump past each other.

When `fast` reaches the end of an acyclic list, `slow` is exactly in the middle.

## Template (Floyd's cycle detection)
```
slow = fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
    if slow is fast:
        # cycle found; to find its start:
        p = head
        while p is not slow:
            p, slow = p.next, slow.next
        return p
return None                        # no cycle
```

## Worked example
**Linked List Cycle II (LC 142)** on `1 → 2 → 3 → 4 → 5`, where `5` points back to `3`.

```
1 → 2 → 3 → 4 → 5
        ↑       │
        └───────┘
```

Phase 1, find a meeting point:

| step | slow | fast | met? |
|:---:|:---:|:---:|:---:|
| 0 | 1 | 1 | |
| 1 | 2 | 3 | no |
| 2 | 3 | 5 | no |
| 3 | 4 | 4 | **yes** |

Phase 2, reset one pointer to the head and move both one step at a time:

| step | p (from head) | slow (from meeting point) |
|:---:|:---:|:---:|
| 0 | 1 | 4 |
| 1 | 2 | 5 |
| 2 | **3** | **3** |

The cycle starts at **3**. This works because the distance from the head to the cycle start equals the distance from the meeting point forward to the cycle start, modulo the cycle length.

## Classic problems
- Linked List Cycle (LC 141)
- Linked List Cycle II (LC 142)
- Middle of the Linked List (LC 876)
- Happy Number (LC 202)
- Find the Duplicate Number (LC 287)

## Complexity
Time O(n). Space O(1), which is the whole point compared with a visited set.

## Common mistakes
- **Checking `fast.next.next` without checking `fast.next`.** The loop condition must be `fast and fast.next`, or you dereference null on even-length lists.
- **Comparing values instead of nodes.** Two different nodes can hold the same value. Compare identity.
- **Stopping after phase 1.** Meeting proves a cycle exists; it does not tell you where it starts. That needs phase 2.
- **Off-by-one on the middle.** On an even-length list, decide whether you want the first or second middle and start `fast` accordingly.

## vs Two Pointers
Classic [two pointers](two-pointers.md) usually move toward each other on sorted data. Fast and slow pointers move the same direction at different speeds, and the speed difference is what carries the information.

## See it run
Watch both pointers race around the list until the fast one laps the slow one: ▶ https://tryexpora.com/algorithm-debugger
