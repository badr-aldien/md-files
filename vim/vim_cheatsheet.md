# Vim in VSCode Cheatsheet

## Modes

- `Esc` - Enter Normal mode
- `i` - Enter Insert mode (before cursor)
- `a` - Enter Insert mode (after cursor)
- `v` - Enter Visual mode (character selection)
- `V` - Enter Visual Line mode (line selection)
- `Ctrl+v` - Enter Visual Block mode (block selection)

## Basic Navigation

- `h` - Move left
- `j` - Move down
- `k` - Move up
- `l` - Move right
- `w` - Move forward to start of next word
- `b` - Move backward to start of previous word
- `e` - Move to end of word
- `0` - Move to beginning of line
- `^` - Move to first non-blank character of line
- `$` - Move to end of line
- `gg` - Go to first line of document
- `G` - Go to last line of document
- `{number}G` - Go to specific line number (e.g., `25G` goes to line 25)
- `:{number}` - Go to specific line number (e.g., `:25` goes to line 25)
- `Ctrl+d` - Move down half a page
- `Ctrl+u` - Move up half a page
- `Ctrl+f` - Move down one page
- `Ctrl+b` - Move up one page

## Editing

- `i` - Insert before cursor
- `I` - Insert at beginning of line
- `a` - Append after cursor
- `A` - Append at end of line
- `o` - Open new line below current line
- `O` - Open new line above current line
- `x` - Delete character under cursor
- `X` - Delete character before cursor
- `dd` - Delete entire line
- `D` - Delete from cursor to end of line
- `dw` - Delete word from cursor
- `db` - Delete word backward
- `d$` - Delete to end of line
- `d0` - Delete to beginning of line
- `u` - Undo
- `Ctrl+r` - Redo
- `.` - Repeat last command

## Copying (Yanking) and Pasting

- `yy` - Copy (yank) entire line
- `Y` - Copy entire line (same as `yy`)
- `yw` - Copy word from cursor
- `y$` - Copy to end of line
- `y0` - Copy to beginning of line
- `yiw` - Copy inner word (word under cursor)
- `yaw` - Copy a word (includes surrounding whitespace)
- `p` - Paste after cursor
- `P` - Paste before cursor
- `{number}yy` - Copy multiple lines (e.g., `3yy` copies 3 lines)

## Cutting (Deleting to Register)

Note: In Vim, deleting also copies to the register, so you can paste it.

- `dd` - Cut entire line
- `dw` - Cut word
- `d{motion}` - Cut based on motion

## Visual Mode Operations

- `v` - Start visual mode, select characters
- `V` - Start visual line mode, select lines
- `Ctrl+v` - Start visual block mode
- `y` - Yank (copy) selected text
- `d` - Delete selected text
- `c` - Change selected text (delete and enter insert mode)
- `>` - Indent selected text
- `<` - Unindent selected text

## Search and Replace

- `/pattern` - Search forward for pattern
- `?pattern` - Search backward for pattern
- `n` - Next search result
- `N` - Previous search result
- `*` - Search for word under cursor (forward)
- `#` - Search for word under cursor (backward)
- `:%s/old/new/g` - Replace all occurrences in file
- `:s/old/new/g` - Replace all occurrences in current line
- `:%s/old/new/gc` - Replace all with confirmation

## Working with Multiple Lines

- `{number}dd` - Delete multiple lines (e.g., `3dd` deletes 3 lines)
- `{number}yy` - Copy multiple lines (e.g., `5yy` copies 5 lines)
- `{number}j` - Move down multiple lines
- `{number}k` - Move up multiple lines

## Text Objects

- `ciw` - Change inner word
- `caw` - Change a word (includes whitespace)
- `ci"` - Change inside quotes
- `ca"` - Change around quotes (includes quotes)
- `ci(` or `cib` - Change inside parentheses
- `ca(` or `cab` - Change around parentheses
- `ci{` or `ciB` - Change inside braces
- `ci[` - Change inside brackets

Replace `c` with `d` to delete, or `y` to yank (copy).

## Saving and Quitting

- `:w` - Save file
- `:q` - Quit
- `:wq` or `:x` or `ZZ` - Save and quit
- `:q!` - Quit without saving
- `:wa` - Save all open files

## Indentation

- `>>` - Indent current line
- `<<` - Unindent current line
- `{number}>>` - Indent multiple lines (e.g., `3>>`)
- `={motion}` - Auto-indent
- `gg=G` - Auto-indent entire file

## Window Management (VSCode Specific)

- `Ctrl+w v` - Split window vertically
- `Ctrl+w s` - Split window horizontally
- `Ctrl+w h/j/k/l` - Navigate between windows
- `Ctrl+w c` - Close current window

## Other Useful Commands

- `~` - Toggle case of character under cursor
- `J` - Join current line with next line
- `r{char}` - Replace single character under cursor
- `R` - Enter Replace mode
- `f{char}` - Jump forward to character in line
- `F{char}` - Jump backward to character in line
- `t{char}` - Jump forward to before character
- `T{char}` - Jump backward to after character
- `;` - Repeat last f, F, t, or T command
- `,` - Repeat last f, F, t, or T command in opposite direction
- `%` - Jump to matching bracket/parenthesis
- `zz` - Center cursor on screen
- `zt` - Move cursor to top of screen
- `zb` - Move cursor to bottom of screen

## Tips

- Most commands can be prefixed with a number to repeat them (e.g., `5j` moves down 5 lines)
- Combine operators with motions (e.g., `d3w` deletes 3 words, `y2j` copies current line and 2 lines below)
- In VSCode, you can access VSCode commands while in Normal mode with `Ctrl+Shift+P`