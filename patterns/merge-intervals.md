# Merge Intervals

## Trigger
The input is a list of ranges `[start, end]` that may overlap, and you need to merge them, insert a new one, find free gaps, or count how many are active at the same time (meeting rooms, bookings, CPU tasks).

## How it works
Sort by start. After sorting, an interval can only overlap the one you built just before it, so a single pass is enough: if the next interval starts before the current one ends, extend the current end; otherwise close the current interval and start a new one.

For "how many at once", split each interval into a start event and an end event, sort the events, and sweep with a counter (or keep a min-heap of end times).

## Template (merge)
```
intervals.sort(key=lambda iv: iv[0])
merged = [intervals[0]]
for start, end in intervals[1:]:
    if start <= merged[-1][1]:                  # overlaps
        merged[-1][1] = max(merged[-1][1], end)
    else:
        merged.append([start, end])
```

## Worked example
**Merge Intervals (LC 56)** on `[[1,3], [2,6], [8,10], [9,12], [15,18]]`, already sorted by start.

```
 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18
 [-----]
    [-----------]
                      [-----]
                         [--------]
                                        [--------]
```

| next interval | current merged | overlaps? | action | result so far |
|:---:|:---:|:---:|:---|:---|
| [1,3] | | | start | `[1,3]` |
| [2,6] | [1,3] | 2 ≤ 3, yes | extend end to 6 | `[1,6]` |
| [8,10] | [1,6] | 8 > 6, no | close, start new | `[1,6] [8,10]` |
| [9,12] | [8,10] | 9 ≤ 10, yes | extend end to 12 | `[1,6] [8,12]` |
| [15,18] | [8,12] | 15 > 12, no | close, start new | `[1,6] [8,12] [15,18]` |

Answer: `[[1,6], [8,12], [15,18]]`.

## Classic problems
- Merge Intervals (LC 56)
- Insert Interval (LC 57)
- Non-overlapping Intervals (LC 435)
- Meeting Rooms II (LC 253)
- Interval List Intersections (LC 986)

## Complexity
Time O(n log n) for the sort; the merge pass itself is O(n). Space O(n) for the output.

## Common mistakes
- **Not sorting first.** Without the sort, an overlap can hide anywhere in the list.
- **Setting the end to the new end instead of the max.** `[1,10]` followed by `[2,3]` must stay `[1,10]`.
- **Touching intervals.** Decide whether `[1,3]` and `[3,5]` overlap. Merge Intervals says yes (`<=`); meeting rooms usually say no.
- **Sorting by end when you need start** (or the reverse). Merging sorts by start; picking the most non-overlapping intervals sorts by end.

## vs Greedy
Merge Intervals is a greedy algorithm whose greedy choice only becomes safe after the sort. The variants that ask for the fewest removals or the most meetings are greedy too, but they sort by end time, which is the detail that trips people up.

## See it run
Watch the sweep line move across the timeline and each overlap fold into the interval before it: ▶ https://tryexpora.com/algorithm-debugger
