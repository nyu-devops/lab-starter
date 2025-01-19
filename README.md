# NYU DevOps Starter Lab

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This first lab is to ensure that your development environment is working correctly. You should only need to install this software once to be ready for all of the labs in this course.

You can read more about creating these environments in my article: [Creating Reproducable Development Environments](https://johnrofrano.medium.com/creating-reproducible-development-environments-fac8d6471f35)

## Prerequisite Software Installation

This lab uses Docker and Visual Studio Code with the Remote Containers extension to provide a consistent repeatable disposable development environment for all of the labs in this course.

You will need the following software installed:

- [Git](https://git-scm.com/downloads)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Visual Studio Code](https://code.visualstudio.com)
- [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension from the Visual Studio Marketplace

All of these can be installed manually by clicking on the links above or you can use a package manager like **Homebrew** on Mac of **Chocolatey** on Windows.

### Install on macOS using Homebrew

If you are using a Mac it is strongly suggested that you use `homebrew` to manage all of your development tools. If you don't have homebrew you can install it from [brew.sh](http://brew.sh) or just open a `terminal` and use this command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once installed you can install all of the prerequisite software for the labs using these commands:

```bash
xcode-select --install
```

This will install prerequisites for `git`. Then install the tools with:

```bash
brew install git
brew install --cask docker
brew install --cask visual-studio-code
```

You must setup Visual Studio Code as a Mac to launch from the command line using these [instructions](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line). Then you can run the `code` command to install the remote containers extension.

```bash
code --install-extension ms-vscode-remote.remote-containers
```

That's it! You can now [bring up the development environment](#bring-up-the-development-environment).

### Install on Windows using Chocolatey

If you are using a Windows it is strongly suggested that you use `choco` to manage all of your development tools. If you don't have Chocolatey you can find instructions to install it from [chocolatey.org](https://docs.chocolatey.org/en-us/choco/setup)

Open a **Command Prompt** (`cmd`) and then:

```cmd
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Once installed you can install all of the prerequisite software for the labs using these commands:

```bash
choco install git
choco install docker-desktop
choco install vscode
code --install-extension ms-vscode-remote.remote-containers
```

That's it! You can now [bring up the development environment](#bring-up-the-development-environment).

## Bring up the development environment

To bring up the development environment you should clone this repo, change into the repo directory, and then open Visual Studio Code using the `code .` command. VS Code will prompt you to reopen in a container and you should say **yes**. This will take a while as it builds the Docker image and creates a container from it to develop in.

```bash
git clone https://github.com/nyu-devops/lab-starter.git
cd lab-starter
code .
```

Note that there is a period `.` after the `code` command. This tells Visual Studio Code to open the editor and load the current folder of files.

Once the environment is loaded you should be placed at a `bash` prompt in the `/app` folder inside of the development container. This folder is mounted to the current working directory of your repository on your computer. This means that any file you edit while inside of the `/app` folder in the container is actually being edited on your computer. You can then commit your changes to `git` from either inside or outside of the container.

## Bring down the development environment

There is no need to manually bring the development environment down. When you close Visual Studio Code it will wait a while to see if you load it back up and if you don't it will stop the Docker containers. When you come back again, it will start them up and resume where you left off.

If you want to manually close the containers you can use the command pallet and select **Close Remote Connection**. If you want to permanently delete the container you can use Docker commands to:

```bash
docker ps -a
docker stop <container-id>
docker rm <container-id>
```

Where `<container-id>` is the id of the container returned from the `docker ps -a` command.

For Example:

```bash
$ docker ps -a
                                                                                                  (master)
CONTAINER ID   IMAGE                                              COMMAND                  CREATED          STATUS          PORTS      NAMES
d9c94acd264b   vsc-lab-starter-2013d33dfd4af07fa71a13e87cbc6b63   "/bin/sh -c 'echo Co…"   56 minutes ago   Up 56 minutes   5000/tcp   affectionate_elgamal

$ docker stop d9c94acd264b
$ docker rm d9c94acd264b
```

## Explain the role of certain files and folders in the project structure for better understanding

### **.devcontainer/**
- **`devcontainer.json`**: Configuration file for setting up a development container. It defines the development environment, including extensions, settings, and the base image to use (The json file will link to `Dockerfile`).
- **`Dockerfile`**: Defines the container environment, specifying the base image and any dependencies or tools needed for the project.

### **.vscode/**
- **`launch.json`**: Configuration for debugging in Visual Studio Code. It specifies how to launch and debug the application.

### **`.flaskenv`**:
- Stores environment variables for Flask applications. Common variables include `FLASK_APP` (entry point) and `FLASK_ENV` (development or production mode).

### **`.gitattributes`**:
- Specifies file handling rules for Git, such as line endings, file diffing, and merging behavior.

### **`.gitignore`**:
- Lists files and directories to be ignored by Git. Typically includes temporary files, build artifacts, and sensitive information.

### **LICENSE**:
- Indicates the licensing terms for your project. Defines how others can use, modify, and distribute your code.


### **setup.cfg**:
- Configuration file for packaging and distribution of your Python project. Often used with `setuptools`.

## License

Copyright (c) 2020-2024 John Rofrano. All rights reserved.

Licensed under the Apache License. See [LICENSE](LICENSE)

This repo is part of the NYU masters class: **CSCI-GA.2820-001 DevOps and Agile Methodologies** created and taught by [John Rofrano](https://www.linkedin.com/in/JohnRofrano/)
