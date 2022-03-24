# Python

<p align="center"><img align="center" src="assets/python.png"></p>

[Python](https://www.python.org/) is an interpreted high-level general-purpose programming language.

## Index

* [General](#general)
* [Pip](#pip)
* [Virtualenv](#virtualenv)
* [Conda](#conda)

## General

Print the version.
```
python --version
```

Run an HTTP server.
```
python -m http.server 8080
```

## Pip

[Pip](https://pip.pypa.io/en/latest/) is the package installer for Python.

Update.
```
python -m pip install --upgrade pip
```

Install packages.
```
pip install <package>
pip install -r <requirements.txt>
```

Export packages and versions.
```
pip freeze > <requirements.txt>
```

Uninstall package.
```
pip uninstall <package>
```

## Virtualenv

[Virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to create isolated Python environments.

Install.
```
pip install virtualenv
```

Create a virtual environment.
```
python -m venv <env>
```

Activate a virtual environment.
```
source <env>/bin/activate
<env>\Scripts\activate.bat
```

Check Python location.
```
which python
where python
```

Deactivate a virtual environment.
```
deactivate
deactivate.bat
```

## Conda

[Conda](https://conda.io/) is an open source package management system and environment management system.

### General

Show version.
```
conda info
```

Update.
```
conda update conda
```

### Environments

List all the environments.
```
conda info --envs
```

Create a new environment.
```
conda create --name <env> python=<version>
```

Create an environment from a yml file.
```
conda env create --file <environment.yml>
```

Export an environment to a yml file.
```
conda env export > <environment.yml>
```

Clone an environment.
```
conda create --name <new> --clone <old>
```

Activate an environment.
```
source activate <env>
conda activate <env>
```

Deactivate an environment.
```
source deactivate
conda deactivate
```

Remove an environment.
```
conda remove --name <env> --all
```

### Packages

List the packages.
```
conda list
```

Check if a package is installed in an environment.
```
conda list --name <env> <package>
```

Install a new package.
```
conda install <package>
```

Install packages from file.
```
conda install --file requirements.txt
```

Update a package.
```
conda update <package>
```

Remove a package.
```
conda remove <package>
```

### Environment variables

List the environment variables.
```
conda env config vars list
```

Set an environment variable.
```
conda env config vars set <variable>=<value>
```

Unset an environment variable.
```
conda env config vars unset <variable> --name <env>
```

### Issues

Use Conda in PowerShell.
```
conda init powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
