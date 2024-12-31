---
Title: Untitled
Date: 29.07.2023
Time: 20:53
Tags: [cheatsheet]
---

| command                         | description                                             |
| ------------------------------- | ------------------------------------------------------- |
| pipenv --python \<version\>     | Create a new project with a specific Python version     |
| pipenv install                  | Install packages specified in Pipfile                   |
| pipenv install \<package\>      | Install a specific package                              |
| pipenv uninstall \<package\>    | Uninstall a package                                     |
| pipenv update                   | Update all packages                                     |
| pipenv lock                     | Generate a lockfile (Pipfile.lock)                      |
| pipenv shell                    | Activate the virtual environment                        |
| exit                            | Deactivate the virtual environment                      |
| pipenv --rm                     | Remove the virtual environment                          |
| pipenv --venv                   | Print the path to the virtual environment               |
| pipenv graph                    | Show a graph of package dependencies                    |
| pipenv check                    | Check for security vulnerabilities                      |
| pipenv clean                    | Remove unused packages                                  |
| pipenv lock                     | Generate a lockfile (Pipfile.lock)                      |
| pipenv sync                     | Install packages specified in Pipfile.lock              |
| pipenv install --ignore-pipfile | Install packages without using Pipfile                  |
| pipenv install --dev            | Install development packages                            |
| pipenv install --system         | Install packages globally (outside virtual environment) |
| pipenv --where                  | Print the project's root directory                      |
| pipenv --py                     | Print the path to the Python interpreter                |
| pipenv run \<command\>          | Run a command in the virtual environment                |
| pipenv run python \<script.py\> | Run a Python script in the virtual environment          |
|                                 |                                                         |
### Pip check module version in registry
```bash
pip index versions setuptools
```
