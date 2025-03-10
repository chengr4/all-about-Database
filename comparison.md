# Comparison

## LOCK

| \   | NL  | IS | IX | S   | SIX | X |
| --- |---- |-----|----|---|-----|---|
| NL  |  Y  |  Y  | Y | Y |  Y | Y |
| IS  |  Y  |  Y  | **Y** | Y | **Y** | N |
| IX  |  Y  | Y   |   **Y** | N | N |  N|
| S   | Y   | Y   | **N**| Y| N | N|
| SIX | Y   | **Y**   | N  |  N |  N |  N|
| X   | Y   | N   |   N    | N  | N |  N |

## NOT IN vs. NOT EXISTS

### NOT EXISTS

- 檢查子查詢是否返回任何結果。如果子查詢返回任何結果，則 `NOT EXISTS` 返回 `FALSE`，否則返回 `TRUE`
- 子查詢返回多行數據且可能包含 `NULL` 值時，`NOT EXISTS` 是更好的選擇，因為它不會受到 `NULL` 值的影響
- NOT EXISTS 通常比 NOT IN 更高效

### NOT IN



## Join Comparison

| Join Type | Cost | Memory |
|-----------|------|--------|
| Page-oriented nested loops | B(R) + B(R) * B(S) | 3 buffers |
| Block nested loops | B(R) + (B(R)/M-2)B(S) => B(R)B(S)/M | M > 2 |
| Index nested loops (S clustered) | B(R) + (T(R) * index I/O) + B(S) | M > 2 + #buffers for index |
| Index nested loops (S unclustered) | B(R) + (T(R) * index I/O) + T(S) | M > 2 + #buffers for index |
| Two-pass multi-way merge sort | 5B(R) + 5B(S) | B(R) < M(M-1) and B(S) < M(M-1) and M > 2 |
| General multi-way merge sort | 2B(R)(1+log_M-1(B(R)/M)) + 2B(S)(1+log_M-1(B(S)/M)) + B(R) + B(S) | M > 2 |
| Optimized Two-pass multi-way merge sort | 3B(R) + 3B(S) | B(R) + B(S) <= M(M-1), more strict memory than normal one |
| Optimized general multi-way merge sort | ? | M > 2 (I guess) |
| Hash Join | 3B(R) + 3B(S) | B(R)/(M-1) < M, B(R) is smaller than B(S) |

> Usually, index nested loops join is faster than block nested loops join.
