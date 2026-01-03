---
name: Library/vtshly/slash-command-insert-footnote
tags: meta/library

---

# Slash command: footnote

```space-lua
slashCommand.define {
  name = "footnote",
  run = function()
    local footnoteName = editor.prompt("Enter footnote name:", "")
    if not footnoteName or footnoteName == "" then
      return
    end

    -- insert inline footnote at the cursor position
    editor.insertAtCursor("[^" .. footnoteName .. "]", false, true)

    local doc = editor.getText()
    local pattern = "%[%^" .. footnoteName .. "%]:"
    if string.find(doc, pattern) then
      -- footnote already exists, exit
      return
    end

    -- insert footnote at the end of the file
    local endPos = #doc
    local insertFtEnd = "\n\n[^" .. footnoteName .. "]: "
    editor.insertAtPos(insertFtEnd, endPos)

    -- move the cursor to the footnote position at the end of the file
    local cursorPos = endPos + string.len(insertFtEnd)
    editor.moveCursor(cursorPos, true)
  end
}

```
