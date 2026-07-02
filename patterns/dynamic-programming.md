# Dynamic Programming

## Trigger
The problem has overlapping subproblems (the same smaller question is asked again and again) and optimal substructure (the best answer is built from the best answers to smaller pieces). Signals: "count the number of ways", "minimum or maximum cost", "can you reach", and a brute-force recursion that recomputes the same inputs.

## How it works
Define a state that captures everything you need to know at a point. Write the recurrence that builds a state from smaller states. Then either memoize the recursion (top-down) or fill a table in dependency order (bottom-up). The art is choosing the state; the recurrence usually follows.

## Template (bottom-up)
```
dp = [base_case for _ in range(n + 1)]
for i in range(1, n + 1):
    dp[i] = combine(dp[i - 1], dp[i - 2], ...)   # the recurrence
return dp[n]
```

## Top-down is just DFS + memo
```
memo = {}
def solve(state):
    if state in base: return base_value
    if state in memo: return memo[state]
    memo[state] = best(solve(smaller) for each choice)
    return memo[state]
```

## Worked example
**Climbing Stairs (LC 70)** for `n = 5`. You climb 1 or 2 steps at a time; count the distinct ways to reach step `n`. The ways to reach step `i` are the ways to reach `i-1` (then a single step) plus the ways to reach `i-2` (then a double step): `dp[i] = dp[i-1] + dp[i-2]`.

```
step i:   0   1   2   3   4   5
dp[i]:    1   1   2   3   5   8
```

| i | recurrence | dp[i] |
|:---:|:---|:---:|
| 0 | base case (one way: stay put) | 1 |
| 1 | base case | 1 |
| 2 | dp[1] + dp[0] = 1 + 1 | 2 |
| 3 | dp[2] + dp[1] = 2 + 1 | 3 |
| 4 | dp[3] + dp[2] = 3 + 2 | 5 |
| 5 | dp[4] + dp[3] = 5 + 3 | 8 |

Answer: **8**. Each cell is computed once and reused, so the exponential recursion collapses to a single O(n) pass. Because `dp[i]` only looks back two cells, the whole array can even shrink to two variables.

## Classic problems
- Climbing Stairs (LC 70)
- House Robber (LC 198)
- Coin Change (LC 322)
- Longest Increasing Subsequence (LC 300)
- Edit Distance (LC 72)

## Complexity
Time O(number of states x work per transition). Space O(number of states), often reducible to one or two rows when a state depends only on the previous ones.

## Common mistakes
- **Wrong base cases.** Most DP bugs live in `dp[0]` and `dp[1]`, not in the recurrence.
- **Filling in the wrong order.** A cell must be computed after everything it depends on; bottom-up needs the correct loop direction.
- **Forgetting to memoize** the top-down version, which quietly falls back to exponential time.
- **Mis-naming the state.** If the state does not capture everything that affects the future, the recurrence is subtly wrong no matter how clean it looks.

## The hard part
DP is not about the table; it is about naming the state. Ask: what is the smallest set of facts that fully describes where I am? Once the state is right, the recurrence is usually a short case analysis of the choices available.

## See it run
Watch the table fill cell by cell, each value pulling from the smaller states it depends on: ▶ https://tryexpora.com/algorithm-debugger
