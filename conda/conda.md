# Conda

[Conda](https://conda.io/) is an open source package management system and environment management system.

## Basics

Show version.
```
conda info
```

Update.
```
conda update conda
```

## Environments

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

## Packages

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

Update a package.
```
conda update <package>
```

Remove a package.
```
conda remove <package>
```

## Environment variables

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
