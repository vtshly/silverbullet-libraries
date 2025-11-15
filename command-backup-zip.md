---
tags: meta/library

---

# Backup vault: Create Zip Archive

```space-lua
backup = {}

-- Set the directory where backups will be stored.
-- Default is the root of the vault (".").
-- Example: "backups" to store in a "backups" folder.
local BACKUP_DIRECTORY = "."

function backup.zip_vault()
  local timestamp = os.date("%Y%m%d_%H%M%S")
  local filename = "silverbullet_backup_" .. timestamp .. ".zip"
  local full_path = BACKUP_DIRECTORY .. "/" .. filename
  
  print("Creating backup: " .. full_path .. "...")
  -- Check if the directory exists if it's not the current directory
  if BACKUP_DIRECTORY ~= "." then
    local stat_dir = shell.run("stat", {BACKUP_DIRECTORY})
    if stat_dir.code ~= 0 then
      editor.flashNotification("⛔️ Error: Backup directory '" .. BACKUP_DIRECTORY .. "' does not exist.")
      return
    end
  end

  shell.run("zip", {"-r", full_path, ".", "-x", "*.zip"})
  
  local stat_zip = shell.run("stat", {full_path})
  if stat_zip.code == 0 then
    editor.flashNotification("Backup created: " .. full_path)
  else
    editor.flashNotification("⛔️ Error: Failed to create backup file.")
  end
end

command.define {
  name = "Backup: Create Zip Archive",
  run = function()
    backup.zip_vault()
  end
}
```
