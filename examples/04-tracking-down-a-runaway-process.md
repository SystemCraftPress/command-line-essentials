# Example: Tracking Down a Runaway Process

A worked example of the escalation path — from "something's using too much CPU" to actually stopping it, without reaching for the biggest hammer first.

## The Symptom

Your machine is sluggish. You suspect a process is stuck.

## Step 1: See what's running

```bash
ps aux
```

This dumps every process — usually far too much to read directly. Narrow it:

```bash
ps aux | grep node
```

```
dev    48213  97.2  4.1  node build-watcher.js
dev    48390   0.1  0.3  grep node
```

The second line is just the `grep` command matching itself in the process list — normal, and safe to ignore. The first line is the real find: `node build-watcher.js`, using 97.2% CPU, process ID `48213`.

## Step 2: Try a normal stop first

```bash
kill 48213
```

This sends `SIGTERM` — a polite request to shut down. Well-behaved processes catch this signal, clean up (close files, finish a write), and exit on their own.

## Step 3: Confirm it actually stopped

```bash
ps aux | grep node
```

If `48213` is gone from the list, you're done.

## Step 4: If it's still there, escalate

```bash
kill -9 48213
```

`-9` is `SIGKILL` — the process is terminated immediately by the operating system, with no chance to clean up. This is why it's the second step, not the first: a process killed with `-9` mid-write can leave a corrupted file behind.

## The Rule

> Try plain `kill` before `kill -9`.

Reach for `-9` only when a normal `kill` genuinely didn't work — not as a default habit because it's faster.

See the [process lifecycle diagram](../diagrams/process-lifecycle.md) for what these signals actually do at each stage.
