---
tags: meta/library
---

```space-lua
command.define {
  name = "Frontmatter: Add Frontmatter",
  run = function()
    editor.insertAtPos([==[---
title: 
aliases: 
tags: 
source: 

---
|^|
]==], 0, true)
  end
}
```
