# Installing pip/setuptools/wheel with Linux Package Managers

## Fedora

```bash
sudo dnf install python3-pip python3-wheel
```

To learn more about Python in Fedora, please visit the [official Fedora docs](https://developer.fedoraproject.org/tech/languages/python/python-installation.html), [Python Classroom](https://labs.fedoraproject.org/en/python-classroom/) or [Fedora Loves Python](https://fedoralovespython.org/).

## Debian/Ubuntu and derivatives

Firstly, update and refresh repository lists by running this command:

```bash
sudo apt update
sudo apt install python3-venv python3-pip
```

!!! warning "warning"
    Recent Debian/Ubuntu versions have modified pip to use the [“User Scheme”](https://pip.pypa.io/en/stable/user_guide/#user-installs) by default, which is a significant behavior change that can be surprising to some users.

## Arch Linux

```bash
sudo pacman -S python-pip
```
