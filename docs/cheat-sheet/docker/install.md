# Install Docker Engine on Debian

## OS requirements

To install Docker Engine, you need the 64-bit version of one of these Debian versions:

    Debian Bookworm 12 (stable)
    Debian Bullseye 11 (oldstable)

Docker Engine for Debian is compatible with x86_64 (or amd64), armhf, arm64, and ppc64le (ppc64el) architectures.

## Installation methods

You can install Docker Engine in different ways, depending on your needs:

* Docker Engine comes bundled with Docker Desktop for Linux. This is the easiest and quickest way to get started.

* Set up and install Docker Engine from Docker's apt repository.

* Install it manually and manage upgrades manually.

* Use a convenience script. Only recommended for testing and development environments.

### Install using the apt repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker `apt` repository. Afterward, you can install and update Docker from the repository.

1. Set up Docker's `apt` repository.
    ```bash
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
        
    # Add the repository to Apt sources:
    echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```
2. Install the Docker packages.
    To install the latest version, run:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

## Linux post-installation steps for Docker Engine

These optional post-installation procedures describe how to configure your Linux host machine to work better with Docker.

### Manage Docker as a non-root user

The Docker daemon binds to a Unix socket, not a TCP port. By default it's the `root` user that owns the Unix socket, and other users can only access it using `sudo`. The Docker daemon always runs as the `root` user.

If you don't want to preface the `docker` command with `sudo`, create a Unix group called `docker` and add users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group. On some Linux distributions, the system automatically creates this group when installing Docker Engine using a package manager. In that case, there is no need for you to manually create the group.

!!! warning
    The `docker` group grants root-level privileges to the user. For details on how this impacts security in your system, see [Docker Daemon Attack Surface](https://docs.docker.com/engine/security/#docker-daemon-attack-surface).

To create the `docker` group and add your user:

1. Create the `docker` group.
    ```bash
    sudo groupadd docker
    ```

2. Add your user to the docker group.
    ```bash
    sudo usermod -aG docker $USER
    ```

3. Log out and log back in so that your group membership is re-evaluated.
    You can also run the following command to activate the changes to groups:
    ```bash
    newgrp docker
    ```

4. Verify that you can run docker commands without sudo.
    ```bash
    docker run hello-world
    ```

### Configure Docker to start on boot with systemd

Many modern Linux distributions use systemd to manage which services start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distributions using systemd, run the following commands:

```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

To stop this behavior, use disable instead.

```bash
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```


    
    
