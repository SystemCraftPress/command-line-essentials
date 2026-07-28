# Command Line Quick Reference

Command lookup tables for daily terminal use, with PowerShell equivalents. From the [Command Line Essentials Companion Guide](../README.md).

## Navigation and Files

| Task | Command |
|------|---------|
| Print working directory | `pwd` |
| List contents | `ls -la` |
| Change directory | `cd path` |
| Go up one level | `cd ..` |
| Go home | `cd ~` |
| Create a directory (with parents) | `mkdir -p path` |
| Create an empty file | `touch file` |
| Copy a file | `cp source dest` |
| Copy a directory | `cp -r source dest` |
| Move or rename | `mv old new` |
| Delete a file | `rm file` |
| Delete a directory | `rm -r dir` |

## Reading and Searching

| Task | Command |
|------|---------|
| Print a whole file | `cat file` |
| Page through a file | `less file` |
| First 10 lines | `head file` |
| Last 10 lines | `tail file` |
| Follow a growing file | `tail -f file` |
| Search file contents | `grep "text" file` |
| Search recursively | `grep -r "text" dir/` |
| Find files by name | `find . -name "*.py"` |
| Count lines | `wc -l file` |

## Redirection and Pipes

| Symbol | Meaning |
|--------|---------|
| `>` | Redirect stdout, overwrite |
| `>>` | Redirect stdout, append |
| `2>` | Redirect stderr |
| `2>&1` | Merge stderr into stdout |
| `|` | Pipe: feed one command's output into the next |
| `&&` | Run next command only if this one succeeds |
| `;` | Run next command regardless |
| `||` | Run next command only if this one fails |

## Permissions and Processes

| Task | Command |
|------|---------|
| Make a file executable | `chmod +x file` |
| Change owner | `sudo chown user file` |
| List running processes | `ps aux` |
| Stop a process | `kill PID` |
| Force-stop a process | `kill -9 PID` |
| Run in background | `command &` |
| List background/paused jobs | `jobs` |
| Resume most recent job | `fg` |

## Environment and Configuration

| Task | Command |
|------|---------|
| Print a variable | `echo $VAR` |
| Set a variable for this session | `export VAR=value` |
| Create a shortcut | `alias name="command"` |
| Reload shell config | `source ~/.bashrc` |
| Search command history | Ctrl+R |
| Re-run last command | `!!` |

## bash to PowerShell

| Task | bash | PowerShell |
|------|------|------------|
| List contents | `ls -la` | `Get-ChildItem -Force` (or `ls`) |
| Change directory | `cd path` | `Set-Location path` (or `cd`) |
| Print working directory | `pwd` | `Get-Location` (or `pwd`) |
| Copy | `cp -r source dest` | `Copy-Item -Recurse source dest` |
| Move / rename | `mv old new` | `Move-Item old new` |
| Delete | `rm -r dir` | `Remove-Item -Recurse dir` |
| Print a file | `cat file` | `Get-Content file` |
| Search file contents | `grep "text" file` | `Select-String "text" file` |
| Environment variable | `echo $VAR` | `echo $env:VAR` |
| Set environment variable | `export VAR=value` | `$env:VAR = "value"` |
| Process list | `ps aux` | `Get-Process` |
| Stop a process | `kill PID` | `Stop-Process -Id PID` |

> This table covers the commands used in this guide, not the whole of PowerShell — enough to translate what you've learned here, not a second complete reference.

---

For the "why" behind these — plus scenario-based troubleshooting for when things go wrong — see the [Command Line Essentials Companion Guide](../README.md#get-the-full-companion-guide).
