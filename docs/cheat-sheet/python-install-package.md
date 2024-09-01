# Installing Packages

## Requirements for Installing Packages

This section describes the steps to follow before installing other Python packages.

### Ensure you can run Python from the command line

Before you go any further, make sure you have Python and that the expected version is available from your command line. You can check this by running:

```bash
python3 --version
```

!!! note
    Due to the way most Linux distributions are handling the Python 3 migration, Linux users using the system Python without creating a virtual environment first should replace the `python` command in this tutorial with `python3` and the `python -m pip` command with `python3 -m pip --user`. Do not run any of the commands in this tutorial with `sudo`: if you get a permissions error, come back to the section on creating virtual environments, set one up, and then continue with the tutorial as written.

### Create a virtual environment

```bash
python3 -m venv tutorial_env
source tutorial_env/bin/activate
```

This will create a new virtual environment in the `tutorial_env` subdirectory, and configure the current shell to use it as the default `python` environment.

Python “Virtual Environments” allow Python packages to be installed in an isolated location for a particular application, rather than being installed globally.

Imagine you have an application that needs version 1 of LibFoo, but another application requires version 2. How can you use both these applications? If you install everything into /usr/lib/python3.6/site-packages (or whatever your platform’s standard location is), it’s easy to end up in a situation where you unintentionally upgrade an application that shouldn’t be upgraded.

Or more generally, what if you want to install an application and leave it be? If an application works, any change in its libraries or the versions of those libraries can break the application.

Also, what if you can’t install packages into the global site-packages directory? For instance, on a shared host.

In all these cases, virtual environments can help you. They have their own installation directories and they don’t share libraries with other virtual environments.

## Use pip for Installing

pip is the recommended installer. Below, we’ll cover the most common usage scenarios. For more detail, see the [pip docs](https://pip.pypa.io/en/latest/), which includes a complete [Reference Guide](https://pip.pypa.io/en/latest/cli/).

```bash
pip install "SomeProject"
```

To install a specific version:

```bash
pip install "SomeProject==1.4"
```

To install a version that’s compatible with a certain version:

```bash
pip install "SomeProject~=1.4.2"
```

In this case, this means to install any version “==1.4.*” version that’s also “>=1.4.2”.

## Upgrading packages

Upgrade an already installed `SomeProject` to the latest from PyPI.

```bash
pip install --upgrade SomeProject
```

## Requirements files

Install a list of requirements specified in a Requirements File.

```bash
pip install -r requirements.txt
```

To write installed package to Requirements file:

```bash
pip freeze > requirements.txt
```

