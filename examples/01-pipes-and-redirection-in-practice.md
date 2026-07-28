# Example: A Real Log-Analysis Pipeline

A worked example combining several commands into one pipeline — the actual point of learning pipes and redirection.

## The Scenario

You have an application log file, `app.log`, and you suspect there's a spike in error responses. You want the top 5 most common error messages, without opening the file.

## Building It Up, One Piece at a Time

**Step 1: confirm errors exist and see what they look like.**

```bash
grep "ERROR" app.log | head -5
```

```
2026-07-28 09:14:02 ERROR Connection timeout to db-primary
2026-07-28 09:14:05 ERROR Connection timeout to db-primary
2026-07-28 09:15:11 ERROR Invalid auth token
2026-07-28 09:16:40 ERROR Connection timeout to db-primary
2026-07-28 09:17:02 ERROR Disk quota exceeded
```

**Step 2: strip the timestamp so identical errors group together.**

```bash
grep "ERROR" app.log | cut -d' ' -f4-
```

```
ERROR Connection timeout to db-primary
ERROR Connection timeout to db-primary
ERROR Invalid auth token
ERROR Connection timeout to db-primary
ERROR Disk quota exceeded
```

**Step 3: count occurrences of each unique line.**

```bash
grep "ERROR" app.log | cut -d' ' -f4- | sort | uniq -c
```

```
      3 ERROR Connection timeout to db-primary
      1 ERROR Disk quota exceeded
      1 ERROR Invalid auth token
```

`uniq -c` only counts *adjacent* duplicates — that's why `sort` has to come first.

**Step 4: sort by count, descending, and take the top 5.**

```bash
grep "ERROR" app.log | cut -d' ' -f4- | sort | uniq -c | sort -rn | head -5
```

**Step 5: save the result instead of just viewing it.**

```bash
grep "ERROR" app.log | cut -d' ' -f4- | sort | uniq -c | sort -rn | head -5 > top-errors.txt
```

## Why Build It This Way

Each `|` in the final pipeline was added and verified one step at a time — you never wrote the five-command chain from scratch and hoped. If step 3's output looked wrong, you'd know immediately it was step 3, not some combination of all five.

See the [pipeline diagram](../diagrams/pipe-and-redirect-flow.md) for how data actually flows through each stage.
