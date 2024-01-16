# Sublime-notes
My notes for using Sublime-text4

# Key-Bindings
`alt+shift+<num>` - set num of collumns\
`ctrl+w` - close tab\
`ctrl+k` then  `ctrl+shift+left/right` - move tab to other collumn

# Fixes
When toggle comment did not work, changing the keybinding to helped.
```JSON
	{ "keys": ["ctrl+keypad_divide"], "command": "toggle_comment", "args": { "block": false } },
	{ "keys": ["ctrl+shift+keypad_divide"], "command": "toggle_comment", "args": { "block": true } },
```
