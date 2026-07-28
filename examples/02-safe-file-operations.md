# Example: Safe File Operations, in Practice

`rm` has no undo. This example is entirely about the habits that make wildcard deletion safe instead of a horror story.

## The Scenario

You want to delete every `.tmp` file in a build directory.

## The Unsafe Way

```bash
cd build
rm *.tmp
```

This is fine — right up until you're in the wrong directory, or `*.tmp` matches something you didn't expect (a file literally named `important.tmp` that wasn't actually temporary).

## The Safe Sequence

**Step 1: confirm where you are.**

```bash
pwd
```

```
/home/dev/projects/myapp/build
```

**Step 2: preview exactly what the wildcard matches, before deleting anything.**

```bash
ls *.tmp
```

```
cache.tmp  output.tmp  session.tmp
```

Three files, all genuinely temporary. Good.

**Step 3: only now, run the delete.**

```bash
rm *.tmp
```

## A Second Example: Deleting a Directory

The same habit, one step more cautious because `-r` deletes recursively:

```bash
pwd
# /home/dev/projects/myapp/build/cache

ls -la
# confirm this really is the disposable cache directory,
# not something that looks similar

cd ..
rm -r cache
```

## Why `ls` Before `rm` Matters More Than It Seems

A wildcard like `*.tmp` is expanded by the shell *before* `rm` ever sees it — `rm` has no idea a wildcard was involved, it just receives a list of filenames. `ls *.tmp` expands the exact same way, which is precisely why running it first shows you the truth: exactly what `rm` is about to receive, with zero risk.

## The Rules

> Check `pwd` before running anything that moves, deletes, or overwrites.

> Preview a wildcard with `ls` before using it with `rm`.

> There is no undo for `rm`. Treat it with real caution.

See the [safe-deletion decision flow](../diagrams/safe-deletion-decision-flow.md) for this as a checklist diagram.
