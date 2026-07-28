# Exercise 3: Write a Backup Script

**Goal:** write a shell script from scratch that validates its input before doing anything destructive or irreversible.

**Time:** ~20 minutes

## Task

Write `cleanup.sh` — a script that deletes all `.log` files older than a given pattern, but **only after confirming with the user.**

Requirements:

1. Take one argument: a directory to clean up.
2. If no argument is given, print usage instructions and exit with a non-zero status.
3. If the given path isn't a directory, print an error and exit.
4. List the `.log` files that would be deleted, and show the count.
5. Ask the user to confirm (`read -p "Delete these N files? (y/n) "`) before actually deleting anything.
6. Only delete if the user answers `y`.
7. Print a summary of what was deleted (or that nothing was deleted, if the user said no).

## Starting Skeleton

```bash
#!/bin/bash
set -e

TARGET_DIR="$1"

# your validation and logic here
```

## Checkpoints

- [ ] Running the script with no arguments prints usage and doesn't attempt anything
- [ ] Running it against a non-existent directory fails with a clear message, before any file operation
- [ ] The script never deletes a file without the user explicitly confirming
- [ ] `chmod +x cleanup.sh` and `./cleanup.sh some-dir` both work as expected

## Stretch Goal

Add a `--dry-run` flag that shows what *would* be deleted without ever prompting or deleting — useful for testing the script safely.

## Reference

See the [backup script example](../../examples/03-a-small-shell-script.md) for the validation pattern this builds on, and the [safe file operations example](../../examples/02-safe-file-operations.md) for why the confirmation step matters.
