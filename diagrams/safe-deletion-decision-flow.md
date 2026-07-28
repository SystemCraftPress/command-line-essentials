# Diagram: The Safe-Deletion Checklist

The habit from [Example 2](../examples/02-safe-file-operations.md), as a flowchart. There is no undo for `rm` — this is the checklist that makes that survivable.

```mermaid
flowchart TD
    A["About to run rm"] --> B["pwd — confirm<br/>where you are"]
    B --> C{"Using a wildcard<br/>like *.tmp?"}
    C -- "Yes" --> D["ls *.tmp first —<br/>preview the exact match"]
    D --> E{"Does the list match<br/>what you expect?"}
    E -- "No" --> F["STOP — refine the<br/>pattern, look again"]
    F --> D
    E -- "Yes" --> G["Run rm"]
    C -- "No, single file/dir" --> H{"Recursive (-r)?"}
    H -- "Yes" --> I["ls -la the target first"]
    I --> G
    H -- "No" --> G
```

The pattern underneath every branch is the same: whatever `rm` is about to receive, look at it first with a non-destructive command.
