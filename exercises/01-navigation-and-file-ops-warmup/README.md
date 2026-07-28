# Exercise 1: Navigation and File Ops Warmup

**Goal:** get fast and comfortable with the commands you'll type dozens of times a day.

**Time:** ~10 minutes

## Setup

```bash
mkdir -p ~/cli-practice/projectA/src
cd ~/cli-practice
```

## Task

1. From `~/cli-practice`, confirm your location with `pwd`.
2. Create a directory structure in one command: `projectB/src`, `projectB/tests`, `projectB/docs` — all at once, using `mkdir -p` with brace expansion: `mkdir -p projectB/{src,tests,docs}`.
3. Create three empty files: `projectB/src/main.py`, `projectB/tests/test_main.py`, `projectB/README.md`.
4. List everything in `projectB`, including hidden files, in long format.
5. Copy `projectA` to `projectC` (recursively — it's a directory).
6. Rename `projectC` to `projectC-backup`.
7. Delete `projectC-backup` entirely.

## Checkpoints

- [ ] Step 2 created three directories with a single `mkdir` call, not three separate calls
- [ ] `ls -la projectB` shows the three files from step 3 plus the three subdirectories
- [ ] Step 5 used `cp -r`, not plain `cp` (which fails on directories)
- [ ] You ran `ls` to confirm `projectC-backup` existed before deleting it in step 7

## Stretch Goal

Use `find ~/cli-practice -name "*.py"` to list every Python file across both projects in one command.

## Reference

The [cheat sheet](../../cheatsheet/command-line-essentials-cheatsheet.md) and [quick reference](../../reference/quick-reference.md) cover every command used here.
