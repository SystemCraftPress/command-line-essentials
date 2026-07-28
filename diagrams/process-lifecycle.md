# Diagram: The Process Kill Escalation Path

The escalation from [Example 4](../examples/04-tracking-down-a-runaway-process.md) — from finding a process to actually stopping it.

```mermaid
flowchart TD
    A["System feels slow"] --> B["ps aux | grep name"]
    B --> C["Identify the PID"]
    C --> D["kill PID<br/>(SIGTERM — polite request)"]
    D --> E{"Still running?"}
    E -- "No — it stopped" --> F["Done"]
    E -- "Yes — still there" --> G["kill -9 PID<br/>(SIGKILL — immediate, no cleanup)"]
    G --> F
```

`SIGTERM` gives a well-behaved process the chance to close files and exit cleanly. `SIGKILL` skips all of that — reach for it only after a plain `kill` has genuinely failed, since a process killed mid-write can leave corrupted output behind.
