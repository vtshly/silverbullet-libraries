---
name: Library/vtshly/command-add-frontmatter
tags: meta/library

---

# Frontmatter: Add Frontmatter

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
