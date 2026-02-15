# CLI Reference: fzf, fd (fd-find), rg (ripgrep), zoxide

This document summarizes the newly installed CLI tools from clis.txt and provides practical command usage with common options (similar to a concise --help).

## fzf (fuzzy finder)

### Overview
- Interactive fuzzy finder for files, command output, and custom lists.
- Typically combined with pipes or shell keybindings.

### Core usage
```bash
# Fuzzy select from a list
printf "alpha\nbravo\ncharlie\n" | fzf

# Fuzzy select files in current directory
fzf

# Fuzzy select files recursively from a directory
find . -type f | fzf
```

### Common options
```bash
# Start with an initial query
fzf --query="src"

# Exact match only
fzf --exact

# Reverse layout (prompt at top)
fzf --layout=reverse

# Show a header
fzf --header="Select an item"

# Preview the selected file (if bat is installed, otherwise use sed/head)
find . -type f | fzf --preview 'sed -n "1,200p" {}'

# Multi-select with tab
find . -type f | fzf --multi
```

### Useful combos
```bash
# Select a file and open in editor
file=$(find . -type f | fzf) && [ -n "$file" ] && ${EDITOR:-vim} "$file"

# Select a git-tracked file
git ls-files | fzf
```

## fd (fd-find)

### Overview
- Fast, user-friendly alternative to find.
- On Debian, binary is typically named `fdfind`.
- You can use `fdfind` directly or symlink `fd` if you prefer.

### Core usage
```bash
# Find files with name containing "report"
fdfind report

# Find files by extension
fdfind -e md

# Find in a specific directory
fdfind report /path/to/search
```

### Common options
```bash
# Case-insensitive search
fdfind -i report

# Exact match (no fuzzy/partial)
fdfind -g "report.txt"

# Search for directories only
fdfind -t d logs

# Search for files only
fdfind -t f report

# Include hidden files and ignore .gitignore
fdfind -H -I pattern

# Exclude a directory
fdfind pattern --exclude node_modules

# Show full path
fdfind pattern -a

# Execute a command for each result
fdfind -e txt -x wc -l
```

### Useful combos
```bash
# Combine fd with fzf
fdfind -t f | fzf

# Find and open
fdfind -e md -x ${EDITOR:-vim} {}
```

## rg (ripgrep)

### Overview
- Fast recursive grep with sensible defaults and .gitignore support.

### Core usage
```bash
# Search for a literal string in the current directory
rg "needle"

# Search in a specific file
rg "needle" path/to/file.txt

# Search only in specific file types
rg "needle" -g "*.md"
```

### Common options
```bash
# Case-insensitive search
rg -i "needle"

# Fixed string (no regex)
rg -F "needle"

# Show line numbers
rg -n "needle"

# Context lines before/after match
rg -C 2 "needle"

# Only list filenames with matches
rg -l "needle"

# Invert match (show lines that do NOT match)
rg -v "needle"

# Include hidden files and ignore .gitignore
rg --hidden --no-ignore "needle"

# Search in a specific directory
rg "needle" /path/to/search
```

### Useful combos
```bash
# Pipe matches into fzf for selection
rg -n "needle" | fzf

# Count matches
rg -c "needle"
```

## zoxide

### Overview
- Smarter `cd` with automatic directory ranking based on usage.
- Needs shell init to enable `z` and `zi`.

### Shell setup (bash)
```bash
# Add to ~/.bashrc
export PATH="$HOME/.local/bin:$PATH"
eval "$(zoxide init bash)"
```

### Shell setup (zsh)
```bash
# Add to ~/.zshrc
export PATH="$HOME/.local/bin:$PATH"
eval "$(zoxide init zsh)"
```

### Core usage
```bash
# Jump to a directory by fuzzy rank
z project

# Jump with interactive selection
zi project

# Add a directory explicitly
zoxide add /path/to/dir

# Remove a directory from the database
zoxide remove /path/to/dir

# Show current database entries
zoxide query -l
```

### Common options
```bash
# Show best match only
zoxide query project

# Show interactive query (fzf-style, if installed)
zoxide query -i

# Show output suitable for scripting
zoxide query --json
```

## Notes
- On Debian, `fd` is `fdfind`. You can create a symlink if desired:
```bash
mkdir -p ~/.local/bin
ln -s $(command -v fdfind) ~/.local/bin/fd
```
- If you use fzf frequently, consider enabling shell keybindings for history and file completion (see `man fzf`).
