# In-place Linked List Reversal

## Trigger
You need to reverse a linked list, or a section of it, or reorder nodes (reverse every k nodes, check a palindrome), and you must not allocate new nodes or copy values into an array.

## How it works
Walk the list with three pointers: `prev`, `curr` and `next`. At each node, save `next`, point `curr.next` back at `prev`, then move `prev` and `curr` one step forward. When `curr` falls off the end, `prev` is the new head.

To reverse only a section, walk to the node just before it, reverse that many nodes with the same loop, and reconnect both ends. A dummy node in front of the head removes the special case when the section starts at the head.

## Template (whole list)
```
prev = None
curr = head
while curr:
    nxt = curr.next       # 1. save the rest of the list
    curr.next = prev      # 2. flip the arrow
    prev = curr           # 3. step forward
    curr = nxt
return prev               # new head
```

## Worked example
**Reverse Linked List (LC 206)** on `1 → 2 → 3 → 4`. Each step flips one arrow.

| step | prev | curr | next saved | list after the flip |
|:---:|:---:|:---:|:---:|:---|
| start | null | 1 | | `1 → 2 → 3 → 4` |
| 1 | 1 | 2 | 2 | `null ← 1`   `2 → 3 → 4` |
| 2 | 2 | 3 | 3 | `null ← 1 ← 2`   `3 → 4` |
| 3 | 3 | 4 | 4 | `null ← 1 ← 2 ← 3`   `4` |
| 4 | 4 | null | null | `null ← 1 ← 2 ← 3 ← 4` |

`curr` is null, so the loop stops and `prev` (4) is the new head: `4 → 3 → 2 → 1`. At every moment the list is split into a reversed part, starting at `prev`, and an untouched part, starting at `curr`.

## Classic problems
- Reverse Linked List (LC 206)
- Reverse Linked List II (LC 92)
- Reverse Nodes in k-Group (LC 25)
- Palindrome Linked List (LC 234)
- Reorder List (LC 143)

## Complexity
Time O(n). Space O(1) for the iterative version; the recursive version uses O(n) stack.

## Common mistakes
- **Flipping the arrow before saving `next`.** The rest of the list is lost. Save first, always.
- **Returning `head` instead of `prev`.** After the loop, `head` is the tail.
- **Losing the connection on partial reversal.** Keep a pointer to the node before the section and to the section's first node, which becomes its last.
- **No dummy node.** Reversing from position 1 then needs its own branch.

## vs Fast & Slow Pointers
They often appear together. Palindrome Linked List uses [fast and slow pointers](fast-slow-pointers.md) to find the middle, reverses the second half in place, then compares both halves with O(1) extra space.

## See it run
Watch each arrow flip while prev, curr and next walk the list: ▶ https://tryexpora.com/algorithm-debugger
