# Bash Scripting Conventions

## General Principles

- Write simple, readable, and self-explanatory code.
- Use meaningful names for variables and functions.
- Keep functions short and focused; max 2-3 arguments.
- Minimize comments; use them only for non-obvious logic.
- Ensure robustness with proper error handling.
- Follow security best practices.

## Script Structure

- Start executables with `#!/usr/bin/env bash`.
- Use `set` to ensure compatibility when run as `bash script_name`.
- Shell scripts should be short and simple; rewrite complex ones in structured languages.
- File naming: lowercase with underscores.
- Use `.sh` extension for libraries (non-executable).
- SUID and SGID are forbidden.

## Formatting & Style

- Indent with 2 spaces; max line length: 80 chars.
- Split long pipelines across multiple lines.
- Place `; then` and `; do` on the same line as `if`, `for`, `while`.
- `else`, `fi`, and `done` should be vertically aligned.
- Use `[[…]]` instead of `[ … ]`.
- Use `$(command)` instead of backticks.

## Best Practices

- Quote variables: `"${var}"`, use `"$@"` over `"$*"`.
- Prefer built-in commands over external ones.
- Avoid `eval`; use Bash arrays for lists.
- Check return values and provide informative messages.
- Place functions near the top, below constants.
- Use `local` for function-specific variables.

## Script Execution & Debugging

- Implement a `main` function in complex scripts:

  ```bash
  if [[ "${BASH_SOURCE[0]}" == "${0}" ]]; then
    main "$@"
  fi
  ```

- Support debug mode (`set -x`) and verbose mode (`-v, --verbose`).
- Provide a dry-run mode for complex scripts.

## Error Handling & Traps

- Redirect errors to STDERR.
- Handle signals properly:

  ```bash
  trap_exit() { echo "Cleaning up..."; }
  trap trap_exit EXIT
  ```

## Standard Locations

- Data: `${XDG_DATA_HOME:-$HOME/.local/share}/program_name`
- Cache: `${XDG_CACHE_HOME:-$HOME/.cache}/program_name`
- Config: `${XDG_CONFIG_HOME:-$HOME/.config}/program_name`
- Runtime: `${XDG_RUNTIME_DIR:-$HOME/.runtime}/program_name`

## Utility Functions

- Common helper functions:

  ```bash
  out() { printf "%b\n" "$*"; }
  err() { >&2 printf "%b\n" "$*"; }
  die() { >&2 printf "%b\n" "$*"; exit 1; }
  now() { date -u "+%Y-%m-%dT%H:%M:%S.%NZ"; }
  log() { printf "%s [%d] %s\n" "$(now)" $$ "$*"; }
  ```

## Miscellaneous

- Boolean values: `true`, `false`.
- Date format: UTC, ISO8601 (`YYYY-MM-DD HH:MM:SS+00:00`).
- Use `while` + `case` for option parsing.
- Provide `--version` support:

  ```bash
  readonly VERSION="1.0.0"
  version() { echo "$VERSION"; }
  ```
