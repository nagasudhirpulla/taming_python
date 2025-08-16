# Ruff python linter and code formatter

## Why use a linter and formatter

- Linters and formatters are tools used to maintain consistency in code quality, readability and coding conventions in a code base
- These tools are generally integrated in code editors, CI/CD pipelines, pre-commit hooks

## What is linter

- Linter is a tool that helps to improve the code quality in terms of readability, potential issues, coding standards and best practices
- Linter analyzes the source code but does not run it

## What is a formatter

- A formatter restructures the source code to make it more readable with a defined set of styling conventions
- A formatter does not modify the source code, it just ensures code styling like consistent indentation, line breaks, spacing etc.

## What is Ruff

- Ruff is a python linter and formatter
- It aims to be a drop-in replacement for existing popular linters and formatters like Flake8, isort, and Black
- It is written in rust and is fast compared to other tools

## Install ruff

### Install with uv

```bash
uv tool install ruff
```

### Install with pip

```bash
pip install ruff
```

It can also be installed with pipx

```bash
pipx install ruff
```

- ruff installation can be verified using `ruff version` command

## Run Ruff

### Run Ruff linter

- `ruff check` command will run the ruff linter and shows the linting errors
- `--fix`  flag will fix any fixable linting errors after checking
- `--watch` flag will run the linter in real time if there are any code changes

```bash
# check in current folder
ruff check

# check in a specific folder
ruff check path/to/code/

# check and fix any fixable linting errors
ruff check --fix

# watch for changes in the folder and re-lint
ruff check --watch
```

### Run Ruff formatter

- ruff formatter is a drop-in replacement for `Black` formatter
- `ruff format` formats the files in the current directory
- `ruff format path/to/code/`  formats the files in a specified directory
- `ruff format path/to/file.py` formats only a specific python file

## Configure ruff

- Ruff comes with formatting and linting rules out of the box
- Default ruff configuration can be found at https://docs.astral.sh/ruff/configuration/#__tabbed_1_2
- Ruff can be configured in the `pyproject.toml` file or `ruff.toml` file of the python project folder
- Ruff configuration can be added to a `pyproject.toml` file with section names starting with `tool.ruff`. Example pyproject.toml file can be as follows

```bash
# pyproject.toml file

[tool.ruff.lint]
# 1. Enable flake8-bugbear (`B`) rules, in addition to the defaults.
select = ["E4", "E7", "E9", "F", "B"]

# 2. Avoid enforcing line-length violations (`E501`)
ignore = ["E501"]

# 3. Avoid trying to fix flake8-bugbear (`B`) violations.
unfixable = ["B"]

# 4. Ignore `E402` (import violations) in all `__init__.py` files, and in selected subdirectories.
[tool.ruff.lint.per-file-ignores]
"__init__.py" = ["E402"]
"**/{tests,docs,tools}/*" = ["E402"]

[tool.ruff.format]
# 5. Use single quotes
quote-style = "single"
```

- Example `ruff.toml` is shown below

```toml
# ruff.toml file

[lint]
# 1. Enable flake8-bugbear (`B`) rules, in addition to the defaults.
select = ["E4", "E7", "E9", "F", "B"]

# 2. Avoid enforcing line-length violations (`E501`)
ignore = ["E501"]

# 3. Avoid trying to fix flake8-bugbear (`B`) violations.
unfixable = ["B"]

# 4. Ignore `E402` (import violations) in all `__init__.py` files, and in selected subdirectories.
[lint.per-file-ignores]
"__init__.py" = ["E402"]
"**/{tests,docs,tools}/*" = ["E402"]

[format]
# 5. Use single quotes
quote-style = "single"
```

### Linting rules

- Documentation of all the ruff linting rules can be found at https://docs.astral.sh/ruff/rules/
- By default, ruff linter uses Flake8’s F rules and a subset of pycodestyle’s E rules for linting
- Only specific rules can be enabled using `lint.select`. Specific rules can be ignored from existing rules using `lint.ignore` . Rules can be added on top of existing rules using `lint.extend-select`

```toml
# ruff.toml file

[lint]
select = ["E", "F"]
ignore = ["F401"]
extend-select = ["I"]
```

- In the above example “E” means all the rules starting with “E”, “F” means all rules starting with “F”.

### Formatting rules

- Ruff formatting options can be found at - https://docs.astral.sh/ruff/settings/#format
- If required, specified files can be excluded from formatting as shown below

```toml
# ruff.toml file

[format]
# do not format files in "directory" folder and ".mypy_cache" folder
exclude = ["directory/*.py", ".mypy_cache"]
```

### Configure lint fixing

- Behavior of `ruff fix` command can be configured in the `lint` section as follows

```toml
# ruff.toml file

[lint]
fixable = ["ALL"]
unfixable = ["F401"]
```

The above configuration fixes all errors except F401

### Safe and unsafe fixes

- By default only safe fixes are done by `ruff check --fix` command. To allow unsafe fixes, use the command `ruff check --fix --unsafe-fixes` (not recommended)
- Unsafe fixes can be promoted as safe and safe fixes can be demoted as unsafe as follows

```toml
# ruff.toml file

[lint]
extend-safe-fixes = ["F601"] # promotes F601 as a safe fix
extend-unsafe-fixes = ["UP034"] # demotes UP034 as a safe fix
```

## Ruff VS Code extension

- Instead of using the ruff check of ruff format command, ruff VS Code extension can be used for easy usage. The Ruff VS Code extension can be found at https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff

![ruff_vs_code_extension.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/ruff_vs_code_extension.png?raw=true)

- Configure VS Code to use ruff in editor by using the following in the VS Code user settings json

```json
{
    "hediet.vscode-drawio.resizeImages": null,
    "[python]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "charliermarsh.ruff",
        "editor.codeActionsOnSave": {
            "source.fixAll": "explicit",
            "source.organizeImports": "explicit"
        }
    }
}
```

- `formatOnSave: true` will format the python file automatically when it is saved
- `“defaultFormatter": "charliermarsh.ruff"` will make ruff as the default formatter
- `"source.fixAll": "explicit"` will fix linting issues automatically when python file is saved
- `"source.organizeImports": "explicit"` will organize imports automatically when python file is saved
- Manually format the python file with `Ctrl+Shift+F`
- Manually organize imports with `Shift+Alt+O`
- Manually fix linting issues with `Ctrl+Shift+P` and search for `Ruff: Fix all auto-fixable problems`

# References

- Ruff Linter docs - [The Ruff Linter | Ruff](https://docs.astral.sh/ruff/linter/)
- Ruff formatter docs -[The Ruff Formatter | Ruff](https://docs.astral.sh/ruff/formatter/)
- Ruff linter rules - https://docs.astral.sh/ruff/rules/#legend
- Ruff VS Code extension docs - [astral-sh/ruff-vscode: A Visual Studio Code extension with support for the Ruff linter.](https://github.com/astral-sh/ruff-vscode/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTEyOTE2MTgwXX0=
-->