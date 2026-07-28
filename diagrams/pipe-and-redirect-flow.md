# Diagram: How Data Flows Through a Pipeline

The log-analysis pipeline from [Example 1](../examples/01-pipes-and-redirection-in-practice.md), stage by stage.

```mermaid
flowchart LR
    A["app.log"] -->|"grep 'ERROR'"| B["matching lines"]
    B -->|"cut -d' ' -f4-"| C["message text only"]
    C -->|"sort"| D["grouped duplicates"]
    D -->|"uniq -c"| E["counted, unique lines"]
    E -->|"sort -rn"| F["highest count first"]
    F -->|"head -5"| G["top 5"]
    G -->|"> top-errors.txt"| H["saved to file"]
```

Each `|` hands the previous command's stdout to the next command's stdin — nothing touches disk until the final `>` at the very end. That's why you can verify any stage by temporarily ending the pipeline there and looking at what it prints.
