# Join Comparison

| Join Type | Cost | Memory |
|-----------|------|--------|
| Page-oriented nested loops | B(R) + B(R) * B(S) | 3 buffers |
| Block nested loops | B(R) + (B(R)/M-2)B(S) => B(R)B(S)/M | M > 2 |
| Index nested loops (clustered) | B(R) + (T(R) * index I/O) + B(S) | M > 2 + #buffers for index |
| Index nested loops (unclustered) | B(R) + (T(R) * index I/O) + T(S) | M > 2 + #buffers for index |
| Two-pass multi-way merge sort | 5B(R) + 5B(S) | B(R) < M^2 and B(S) < M^2 and M > 2 |
| General multi-way merge sort | ? | M > 2 |
| Optimized Two-pass multi-way merge sort | 3B(R) + 3B(S) | B(R) + B(S) <= M(M-1), more strict memory than normal one |
| Hash Join | 3B(R) + 3B(S) | B(R)/(M-1) < M, B(R) is smaller than B(S) |

> Usually, index nested loops join is faster than block nested loops join.
