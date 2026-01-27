# pyenv-manager

A collection of shell utilities for managing pyenv installations.

## Features

- **pyenv-list**: List installable or installed Python versions
- **pyenv-stat**: Analyze Python version usage across `.python-version` files
- **pyenv-cleanup**: Find and remove unused Python versions

## Installation

```bash
git clone https://github.com/RyoNakagami/pyenv-manager.git ~/.tool.d/pyenv-manager
```

Add to your shell configuration (`.bashrc` or `.zshrc`):

```bash
export PATH="$HOME/.tool.d/pyenv-manager/bin:$PATH"
```

## Dependencies

- `pyenv` - Python version management
- `fdfind` (fd-find) - Required for `pyenv-stat` and `pyenv-cleanup`
- `jq` - Optional, for pretty JSON output

## Usage

### pyenv-list

List installable or installed Python versions.

```bash
# List standard installable versions (e.g., 3.10.0, 3.11.5)
pyenv-list

# List all installable versions (including anaconda, pypy, etc.)
pyenv-list -a

# List installed versions
pyenv-list --installed
```

### pyenv-stat

Count and display Python version usage statistics.

```bash
# Show version count table
pyenv-stat

# Output:
# Version  Count
# --------------
# 3.11.8      17
# 3.12.3       0
# 3.12.4       5
# ...

# Output as JSON
pyenv-stat -j

# Show repository paths for each version
pyenv-stat --with-path

# JSON with paths
pyenv-stat -j --with-path

# Search specific directory
pyenv-stat -d /path/to/projects
```

### pyenv-cleanup

Find and remove unused Python versions not referenced by any `.python-version` files.

```bash
# Preview unused versions (dry run)
pyenv-cleanup --dry-run

# Output:
# Unused versions (not referenced by any .python-version):
#   3.10.5
#   3.9.7
# [DRY RUN] No versions were removed.

# Remove with confirmation prompt
pyenv-cleanup

# Force remove without confirmation
pyenv-cleanup -f

# Search specific directory
pyenv-cleanup -d /path/to/projects
```

## Options Reference

**pyenv-list:**

| Option         | Description                      |
| -------------- | -------------------------------- |
| `-a`           | Display all installable versions |
| `--installed`  | Show installed versions          |
| `-h, --help`   | Show help message                |

**pyenv-stat:**

| Option         | Description                            |
| -------------- | -------------------------------------- |
| `-d DIR`       | Directory to search (default: ~)       |
| `-j, --json`   | Output in JSON format                  |
| `--with-path`  | Show repository paths for each version |
| `-v`           | Enable verbose output                  |
| `-h, --help`   | Show help message                      |

**pyenv-cleanup:**

| Option         | Description                      |
| -------------- | -------------------------------- |
| `-d DIR`       | Directory to search (default: ~) |
| `-f, --force`  | Remove without confirmation      |
| `--dry-run`    | Show what would be removed       |
| `-v`           | Enable verbose output            |
| `-h, --help`   | Show help message                |

## Project Structure

```ini
pyenv-manager/
├── bin/
│   ├── pyenv-list        # List Python versions
│   ├── pyenv-stat        # Version usage statistics
│   └── pyenv-cleanup     # Remove unused versions
├── lib/
│   └── docstring.sh      # Shared library for help output
├── docs/
│   ├── BRANCH_STRATEGY.md
│   └── VERSIONING_POLICY.md
├── LICENSE
└── README.md
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

Ryo Nakagami
