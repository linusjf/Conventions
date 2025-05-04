# Bash Scripting Conventions

## 1. Philosophy & General Guidelines

- Code should be easy to read and understand.
- Keep the code as simple as possible. Avoid unnecessary complexity.
- Use meaningful names for variables, functions, etc. Names should reveal intent.
- Functions should be small, focused, and ideally not exceed a few lines.
- Only use comments when necessary-strive to make the code self-explanatory.
- When comments are used, they should add useful info not evident from code.
- Comment tricky, non-obvious, interesting, or important parts of your code.
- Properly handle errors and exceptions to ensure robustness.
- Consider security implications and follow security best practices.
- Shell should only be used for small utilities or simple wrapper scripts.
- Avoid aliases in scripts-use functions instead.
- Use semantic versioning (see **Versioning** section below).
- If a script is over 100 lines or uses complex logic, consider a structured language.

## 2. File Structure & Organization

### 2.1 File Layout

- Start each file with a top-level comment describing its contents.
- A copyright notice and author info are optional.
- Executables must start with `#!/usr/bin/env bash` and minimal flags.
- File names: lowercase with optional underscores.
- Constants and environment exports should be uppercase with underscores.
- Executables should have `.sh` extension or none.
- Libraries must have `.sh` extension and not be executable.
- SUID and SGID are forbidden on shell scripts.

### 2.2 Function Organization

- Group all functions together, right below constant declarations.
- No executable code between functions.
- Only includes, `set` statements, and constant declarations may appear before functions.
- Use `main()` if script contains multiple functions.
- Call `main()` wrapped as:

  ```bash
  if [[ "${BASH_SOURCE[0]}" == "${0}" ]];then
    main "$@"
  fi
  ```

## 3. Style Guide

### 3.1 Indentation & Formatting

- Indent with **2 spaces**, no tabs.
- Maximum line length: **80 characters**.
- Break long strings with here-docs or embedded newlines.
- Break long pipelines one per line unless they fit on a single line.

### 3.2 Conditionals and Loops

- Put `; then`, `; do` on same line as `if`, `for`, or `while`.
- `else`, `fi`, and `done` should be on separate, aligned lines.
- Prefer including `in "$@"` in `for` loops for clarity.
- `[[…]]` is preferred over `[ … ]` or `/usr/bin/[`.

### 3.3 Case Statements

- Indent alternatives by 2 spaces.
- One-liners need a space after `)` and before `;;`
- Long/multi-command branches should place `pattern`, actions, and `;;` on separate lines.

## 4. Functions & Comments

### 4.1 Function Naming

- Function names: lowercase with underscores.
- Use `::` to separate libraries.
- Parentheses required after function name.
- `function` keyword is optional but must be used consistently.

### 4.2 Function Comments

- Any function that's not obvious and short must have a header comment.
- All library functions must have header comments.
- Comments should describe:
  - **Globals** used and modified
  - **Arguments** taken
  - **Outputs** to STDOUT/STDERR
  - **Returns** (besides exit status)
- Code should be usable by reading comments without needing to read the code.

## 5. Variables

- Declare function-specific variables with `local`. Remember: Bash uses **dynamic scoping**.
- Avoid modifying these Bash internals:  
  `BASH_VERSION`, `EUID`, `UID`, `PID`, `LINENO`, `FUNCNAME`, etc.
- Avoid using underscore-prefixed vars (`_`, `__`)-they're reserved.
- Quote variables: Prefer `"${var}"` over `"$var"`.
- Use `"$@"` unless `"$*"` is specifically required.
- Capitalize constants and environment variables.

## 6. Error Handling & Exit Codes

- All error messages should go to **STDERR**.
- Always check return values and give informative errors.
- Use `(( … ))` or `$(( … ))` over `let`, `$[ … ]`, or `expr`.

## 7. I/O & Messaging

### 7.1 Output Functions

- `out` for STDOUT
- `err` for STDERR
- `die` for fatal errors + exit
- `big` for banner messages
- `log` logs timestamp + PID
- `now`, `sec`, `zid`, `cmd` utilities

```bash
out() { printf "%b\n" "$*" ; }; export -f out
err() { >&2 printf "%b\n" "$*" ; }; export -f err
die() { >&2 printf "%b\n" "$*" ; exit 1 ; }; export -f die
big() { printf "\n###\n#\n#\ %b\n#\n###\n\n" "$*"; }; export -f big
log() { printf "%b %b %b\n" "$(now)" $$ "$*" ; }; export -f log
now() { date -u "+%Y-%m-%dT%H:%M:%S.%NZ" ; }; export -f now
sec() { date -u "+%s" ; }; export -f sec
zid() { hexdump -n 16 -v -e '16/1 "%02x" "\n"' /dev/random ; }; export -f zid
cmd() { command -v "$1" >/dev/null 2>&1 ; }; export -f cmd
```

## 8. Versioning

```bash
readonly VERSION="1.0.0"
function version() {
  printf "%s\n" "$VERSION"
}
```

- Should be enabled via `--version` flag.

## 9. Script Modes & Flags

- Every script must support:
  - `--debug`: enable debug mode (`set -x`)
  - `--dry-run`: emulate execution
  - `--verbose` or `-v`: print execution details
  - `--quiet` or `-q`: suppress output
- Verbose mode sets a `verbose=true` flag.

## 10. Signal Traps

- Prefer trapping `EXIT`:

  ```bash
  trap_exit() {
    # Cleanup logic
  }

  trap trap_exit EXIT
  ```

- If trapping multiple signals, use `trap_` prefix:

  ```bash
  trap_exit() …
  trap_term() …
  trap_int() …
  trap_hup() …
  ```

## 11. Colors & Output

- Use POSIX escape strings for colors.
- Gate color output:
  - Only color if output is to terminal.
  - Disable if `NO_COLOR` is set or `TERM` is `dumb`.

## 12. Time & Date

- Use **UTC** and **ISO8601** formats:
  - Date: `YYYY-MM-DD` or `YYYY-W##-#`
  - Time: `HH:MM:SS.NNNNNNNNN`
  - Timezone: `+HH:MM`

## 13. File Sourcing

- Safe `include.sh` sourcing:

```bash
if command -v realpath >/dev/null 2>&1; then
  SCRIPT_DIR=$(dirname "$(realpath "$0")")
else
  SCRIPT_DIR=$(cd -- "$(dirname -- "$0")" &> /dev/null && pwd -P)
fi
source "$SCRIPT_DIR/include.sh"
```

## 14. Usage Instructions

- Usage must include examples.
- Include exit code parameter.
- Usage to **STDOUT** if exit code is 0, else **STDERR**.

## 15. Temporary Directories

```bash
temp_home() { out "$(mktemp -d -t "${1:-$(zid)}")"; }; export -f temp_home;
temp_dir() { out "$(temp_home "$program_command")"; };
```

## 16. PostgreSQL Helpers

```bash
psql_user_names() { psql -tAc "SELECT usename FROM pg_catalog.pg_user;" ; }
psql_user_name_exist() { [ "$( psql -tAc "SELECT 1 FROM pg_catalog.pg_user WHERE usename='$1'" )" = '1' ] ; }
psql_database_names() { psql -tAc "SELECT datname FROM pg_database;" ; }
psql_database_name_exist() { [ "$( psql -tAc "SELECT 1 FROM pg_database WHERE datname='$1'" )" = '1' ] ; }
```

## 17. Assertions for Testing

```bash
assert_empty() { [ -z "$1" ] || err "$FUNCNAME[0]}" "$@" ; }; export -f assert_empty
assert_equal() { [ "$1" = "$2" ] || err "${FUNCNAME[0]}" "$@" ; }; export -f assert_equal
```

## 18. Runtime Directories (XDG)

- **Data**:
  - Use `XDG_DATA_HOME`, else `$HOME/.local/share/$program`
- **Cache**:
  - Use `XDG_CACHE_HOME`, else `$HOME/.cache/$program`
- **Config**:
  - Use `XDG_CONFIG_HOME`, else `$HOME/.config/$program`
- **Runtime**:
  - Use `XDG_RUNTIME_HOME`, else `$HOME/.runtime/$program`

## 19. Miscellaneous

- Prefer `$(command)` over backticks.
- Avoid `eval`.
- Use bash arrays to avoid quoting complications.
- Prefer built-ins over external commands.
- Use process substitution or `readarray` over `while` + pipes.
