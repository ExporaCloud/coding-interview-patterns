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

## Classic problems
- Climbing Stairs (LC 70)
- House Robber (LC 198)
- Coin Change (LC 322)
- Longest Increasing Subsequence (LC 300)
- Edit Distance (LC 72)

## Complexity
Time O(number of states x work per transition). Space O(number of states), often reducible to one or two rows when a state depends only on the previous ones.

## The hard part
DP is not about the table; it is about naming the state. Ask: what is the smallest set of facts that fully describes where I am? Once the state is right, the recurrence is usually a short case analysis of the choices available.

## See it run
Watch the table fill cell by cell, each value pulling from the smaller states it depends on: ▶ https://tryexpora.com/algorithm-debugger
