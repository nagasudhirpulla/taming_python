# uv for all-in-one python project management

## What is a uv

- uv is an all-in-one project management tool for python projects
- It manages python versions, virtual environments, package dependencies automatically for a python project

## Install uv

- uv can be installed in windows using the following command

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

- uv can be installed in linux environments using the following command

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

- uv can also be installed using pipx or pip using the following commands

```bash
pipx install uv
```

## Update uv

- uv can be updated using the following command

```powershell
uv self upgrade
```

- If uv is installed with pipx, it can be updated with the following command

```powershell
pipx upgrade uv
```

## Initialize a new project in a folder

- Run the following to initialize a new uv project inside a folder

```powershell
uv init
uv sync
```

- This will create
    - `pyproject.toml` file - contains project metadata like package versions, name, description, readme file location
    - **`.python-version` file** - specifies the python version used by the project. Python will be installed if not already installed in the OS
    - `uv.lock` file - contains the exact resolved versions that are installed in the project environment. This ensures reproducible virtual environments in all the machines
    - `README.md` file - a README file for project documentation
    - `.gitignore` file - specifies files to be ignored by git

## Managing packages in uv

- uv uses vitual environment in the project folder (`.venv` folder) to manage python packages for the project.
- New packages can be added using `uv add` command. For example, `uv add pandas requests` will add pandas and requests packages to the project
- packages can be removed using `uv remove` command. For example, `uv remove requests` will remove requests package from the project
- `uv add -r requirements.txt` command will add packages mentioned in requirements.txt file into the project. This command is especially to migrate conventional virtual environment based project to a uv project.
- `uv add` and `uv remove` commands will also update the `uv.lock` and `pyproject.toml` files

## Running uv project

- Run entrypoint python script of the uv project using the following command

```powershell
uv run main.py
```

- This command will use the virtual environment and run the python script

## Changing packages in pyproject.toml

- A sample `pyproject.toml` file can be as follows

```toml
[project]
name = "python-command-runner"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.12"
dependencies = [
    "flask>=3.1.1",
    "flask-socketio>=5.5.1",
    "python-socketio[client]>=5.13.0",
]
```

- Adddition, deletion, modification of python dependencies can be done in the dependencies variable of the project section of the `pyproject.toml` file
- After updating `pyproject.toml` file, `uv sync` command should be run to update the virtual environment and uv.lock file

## Upgrade packages

- Packages can be upgraded using `uv lock --upgrade` and then running `uv sync` to update the virtual environment as per the new `uv.lock` file
- `uv lock --upgrade` works only if the dependencies in the `pyproject.toml` are mentioned something like `pandas>=2.3.1`. If a strict dependency version is mentioned (like pandas==2.3.1), upgrade will not be possible.

## References

- uv GitHub repository - https://github.com/astral-sh/uv
- uv official documentation - https://docs.astral.sh/uv/
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjI1ODc1MThdfQ==
-->