---
layout: default
title: Installation
nav_order: 2
permalink: /installation
---
# Installation Guide

{: .note }
This is an installation guide for Unix-based systems. If you are on Windows, I would suggest to use a Docker Container. A guide to install and create a Docker container is in the [Docker Container Setup and Installation Section](#docker-container-setup-and-installation).

This part of the tutorial will be going over the options and how you can install CoquiTTS on your machine or a Docker container.
## Local Installation
To install CoquiTTS, all we need to do is to simply clone the CoquiTTS repository.
```
$ git clone https://github.com/coqui-ai/TTS
```
After running that command above to clone the TTS repository, we should see a folder called TTS. That is the folder we will be working in. More about it will be in the [training](training) section of this tutorial.
## Docker Container Setup and Installation

{: .note }
This section will only go over the necessary parts of a Docker container for this project. If you wish to learn more about Docker containers and how to customize a Docker container to your purposes please checkout the [Docker docs](https://docs.docker.com/)!

If you don't have Docker already installed, I would suggest refering to the [installation guide](https://docs.docker.com/engine/install/) in the Docker docs to get you started.

To create our Docker container:
```
$ docker run -it --name chinese-TTS-model ubuntu
```
This command will create a new Docker container with the name of "Chinese-TTS-model" and attach the container to your terminal.

Later, after you exited out of the Docker container and would like to get back to your container you can run:
```
$ docker start chinese-TTS-model
```
Then you can either attach the container (if you want interactivity), or you can run commands to your container using `exec` (if you don't need interactivity)
```
$ docker attach chinese-TTS-model # to attach the container or
$ docker exec <container-name> <command> # to run command using exec
```
Once you have your Docker container created and ready to go, you can follow the [local installation](#local-installation) section of this page.
