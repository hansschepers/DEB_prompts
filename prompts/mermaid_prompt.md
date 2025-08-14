
For mermaid diagrams, use rstudio-compatible syntax:

- Start with `graph TD` (not `flowchart TD`)  
- Use quotes inside all node objects: `["text"]`, `{"decision?"}`, `("process")`
- Do NOT use quotes in subgraph titles: `subgraph Title Name` (not `"Title Name"`)
- Replace all Greek symbols with normal letters: `d` instead of `δ` or `∂`
- When using special characters in labels, use quotes around the entire label

- use `<BR>` instead of `\n` to make line breaks, and break long lines at ~20 characters.
- when using colored boxes in mermaid, use darker colors, since the text inside them is not standing out
- subgraph labels (titles) should not contain any special characters, NOR have quotes

- do not give a node / vertex to the "MATLAB native functions"