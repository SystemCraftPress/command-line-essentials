# Command Line Essentials Cheat Sheet

A free, printable one-page reference for the terminal. Pulled straight from the [Command Line Essentials Companion Guide](../README.md).

## Navigation and Files

| Task | Command |
|------|---------|
| Where am I | `pwd` |
| List (detailed, hidden) | `ls -la` |
| Change directory | `cd path` / `cd ..` / `cd ~` |
| Make directory (+parents) | `mkdir -p path` |
| Create empty file | `touch file` |
| Copy | `cp source dest` / `cp -r` for dirs |
| Move / rename | `mv old new` |
| Delete | `rm file` / `rm -r dir` |

## Reading and Searching

| Task | Command |
|------|---------|
| Page through a file | `less file` |
| First / last lines | `head file` / `tail file` |
| Follow a growing file | `tail -f file` |
| Search contents | `grep -rin "text" dir/` |
| Find by name | `find . -name "*.py"` |
| Count lines | `wc -l file` |

## Redirection and Pipes

| Symbol | Meaning |
|--------|---------|
| `>` / `>>` | Overwrite / append stdout |
| `2>` | Redirect stderr |
| `|` | Pipe output to next command |
| `&&` / `;` / `||` | Then (if ok) / then (always) / then (if failed) |

## Permissions and Processes

| Task | Command |
|------|---------|
| Make executable | `chmod +x file` |
| List processes | `ps aux` |
| Stop / force-stop | `kill PID` / `kill -9 PID` |
| Run in background | `command &` |
| List jobs / resume | `jobs` / `fg` |

## Environment and Config

| Task | Command |
|------|---------|
| Set for this session | `export VAR=value` |
| Shortcut | `alias name="command"` |
| Reload config | `source ~/.bashrc` |
| Re-run last command | `!!` |

## Script Skeleton

```bash
#!/bin/bash
for file in *.txt; do
  echo "Processing $file"
done
```

## Golden Rules

> Check `pwd` before running anything that moves, deletes, or overwrites.

> Preview a wildcard with `ls` before using it with `rm`.

> There is no undo for `rm`. Treat it with real caution.

> No spaces around `=` in a variable assignment.

> Try plain `kill` before `kill -9`.

---

Want the reasoning behind every one of these rules — plus shell scripting, environment configuration, and a full troubleshooting guide? See the [Command Line Essentials Companion Guide](../README.md#get-the-full-companion-guide).
