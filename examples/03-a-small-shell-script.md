# Example: A Small, Real Shell Script

A backup script — simple enough to fully understand, useful enough to actually keep.

## The Script

```bash
#!/bin/bash

# backup.sh — copies a project directory into a timestamped backup folder

set -e  # exit immediately if any command fails

SOURCE_DIR="$1"
BACKUP_ROOT="$HOME/backups"

if [ -z "$SOURCE_DIR" ]; then
  echo "Usage: ./backup.sh <directory-to-back-up>"
  exit 1
fi

if [ ! -d "$SOURCE_DIR" ]; then
  echo "Error: '$SOURCE_DIR' is not a directory."
  exit 1
fi

TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")
DEST="$BACKUP_ROOT/$(basename "$SOURCE_DIR")_$TIMESTAMP"

mkdir -p "$BACKUP_ROOT"
cp -r "$SOURCE_DIR" "$DEST"

echo "Backed up '$SOURCE_DIR' to '$DEST'"
```

## Running It

```bash
chmod +x backup.sh
./backup.sh ~/projects/myapp
```

```
Backed up '/home/dev/projects/myapp' to '/home/dev/backups/myapp_2026-07-28_09-30-15'
```

## Reading It Line by Line

- **`set -e`** — stop immediately on any failed command, instead of plowing ahead with a partially-broken state. For a script that touches the filesystem, this matters.
- **`SOURCE_DIR="$1"`** — the first command-line argument. Quoted, so a path with spaces doesn't break the script.
- **The two `if` checks** — fail loudly and immediately with a clear message, rather than letting `cp` fail later with a confusing error.
- **`$(date +"%Y-%m-%d_%H-%M-%S")`** — command substitution: the output of `date` becomes part of the string, giving each backup a unique, sortable folder name.
- **`mkdir -p`** — creates `$BACKUP_ROOT` if it doesn't exist yet, and does nothing (without erroring) if it already does.

## What Makes This a Good First Script

It does one thing, it validates its input before acting, and it fails with a message a human can act on instead of a cryptic error three lines deep. That's the actual bar for "good script" — not cleverness.

See the [script skeleton in the cheat sheet](../cheatsheet/command-line-essentials-cheatsheet.md#script-skeleton) for the minimal loop pattern this builds on.
