# Exercise 2: Build a Log-Analysis Pipeline

**Goal:** build a multi-stage pipeline one piece at a time, the same way the [worked example](../../examples/01-pipes-and-redirection-in-practice.md) did — verifying each stage before adding the next.

**Time:** ~15 minutes

## Setup

Create a sample log file:

```bash
cat > access.log << 'EOF'
2026-07-28 09:01:02 GET /home 200
2026-07-28 09:01:05 GET /api/users 200
2026-07-28 09:01:07 GET /api/orders 500
2026-07-28 09:01:09 GET /home 200
2026-07-28 09:01:12 GET /api/orders 500
2026-07-28 09:01:14 GET /login 404
2026-07-28 09:01:16 GET /api/orders 500
2026-07-28 09:01:20 GET /login 404
EOF
```

## Task

Build a pipeline, verifying each stage before adding the next:

1. Find all lines with a `500` status code.
2. From those, extract just the path (4th field).
3. Count how many times each path appears.
4. Sort by count, descending.
5. Redirect the final result to a file called `500-errors-by-path.txt`.

Don't write the whole pipeline at once — run stage 1 alone, confirm the output, then add stage 2, and so on.

## Expected Final Output

```
      3 /api/orders
```

## Checkpoints

- [ ] You verified at least 3 of the 5 stages independently before chaining further
- [ ] Your final command uses `>` exactly once, at the very end
- [ ] `500-errors-by-path.txt` exists and contains the expected line

## Stretch Goal

Extend the pipeline to also report the top `404` path, and write both results to the same file using `>>` for the second one (append, not overwrite).

## Reference

See the [pipeline example](../../examples/01-pipes-and-redirection-in-practice.md) and the [pipeline diagram](../../diagrams/pipe-and-redirect-flow.md).
