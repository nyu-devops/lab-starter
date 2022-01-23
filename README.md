# lab-starter

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

This is first lab to ensure that your development environment is working correctly

## Prerequisite Software Installation

This lab uses Docker and Visual Studio Code with the Remote Containers extension to provide a consistent repeatable disposable development environment for all of the labs in this course.

You will need the following softwrae installed:

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Visual Studio Code](https://code.visualstudio.com)
- [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension from the Visual Studio Marketplace

All of these can be installed manually by clicking on the links above or you can use a package manager like **Homebrew** on Mac of **Chocolatey** on Windows.

### Install on macOS using Homebrew

If you are using a Mac it is strongly suggested that you use `homebrew` to manage all of your development tools. If you don't have homebrew you can install it from [brew.sh](http://brew.sh) or just use this command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once installed you can install all of the prerequisite software for the labs using these commands:

```bash
brew install git
brew install --cask docker
brew install --cask visual-studio-code
```

You must setup Visual Studio Code as a Mac command line interface using these [instructions](https://code.visualstudio.com/docs/setup/mac). Then you can run the `code` comamnd to install the remote containers extension.

```bash
code --install-extension ms-vscode-remote.remote-containers
```

That's it! You can now [bring up the development environment](#bring-up-the-development-environment).

### Install on Windows using Chocolatey

If you are using a Windows it is strongly suggested that you use `choco` to manage all of your development tools. If you don't have Chocolatey you can find instructions to install it from [chocolatey.org](https://docs.chocolatey.org/en-us/choco/setup)

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

To bring up the development environment you should close this repo, change into the repo directory, and then open Visual Studio Code. VS Code will prompt you to reopen in a container and you should say **yes**. This will take a while as it builds the Docker image and creates a container from it to develop in.

```bash
git clone https://github.com/nyu-devops/lab-starter.git
cd lab-starter
code .
```

Note that there is a period `.` after the `code` command. This tells Visual Studio Code to open the editor and load the current folder of files.

Once the environment is loaded you should be placed at a `bash` prompt in the `/app` folder inside of the development container which is mounted to the current working directory of your repository on your computer. This means that any file you edit while inside of the container is actually being edited on your computer.

## Bring down the development environment

There is no need to manually bring the development environment down. When you close Visual Studio Code it will wait a while to see if you load it back up and if you don't it will stop the Docker containers. When you come back again, it will start tem up and resume where you left off.

If you want to manually close the containers you can use the command pallet and select **Close Remote Connection**. If you want to permanently delete the container you can use Docker commands to:

```bash
docker ps -a
docker stop <container-id>
docker rm <container-id>
```

Where `<container-id>` is the id of the container returned from the `docker ps -a` command.

## Copyrights

This repo is part of the NYU masters class: **CSCI-GA.2820-001 DevOps and Agile Methodologies** created by *John Rofrano*. All material is copyright (c) 2022 John Rofrano, All rights reserved.
