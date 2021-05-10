============
Introduction
============

We have setup a container-based development environment to help researchers develop software for their projects. This development environment includes commonly used IDEs including PyCharm, Visual Studio Code, and JupyterLab and can be run on Linux, Mac, or Windows. This provides a replicable sandboxed environment for you to develop your software. For more information, see the software development environment section of the beginner tutorials.

This documentation describes how to:

- setup the container-based development-environment;

- run IDEs from within the development-environment;

- install additional dependencies that your program may require (e.g. third-party python libraries); and

- develop your software project within the development-environment.


Benefits of container-based development
=======================================

Tools such as VMware or VirtualBox have enabled users to create `Virtual machines <https://en.wikipedia.org/wiki/Virtual_machine>`_ to run different operating systems from their computer's native operating system. For example, a user could have Windows running natively on their computer (we will call this the host operating system), but with these tools, they can load an entirely different operating system on their host machine (for example a specific version of Linux). This is achieved by creating a new set of virtual hardware (e.g. cpu's, memory, hard drives, usb controllers, etc) upon which a virtual operating system is run. While being versatile, these virtual machines are resource intensive and have relatively lengthy bootup times (minutes).

`Docker <https://www.docker.com/why-docker>`_ on the other hand is a similar tool that allows a user to create a virtualised operating system. However, rather than creating new virtualised hardware on which to run this virtual operating system, it runs the virtual operating system directly on the host machines hardware. This significantly reduces the memory and storage footprints compared with traditional virtual machines, and also reduces bootup times to a few seconds. The Docker tool enables you to prebuild light-weight operating systems along with any programs of interest and store them as Docker images (e.g. webservers, Jupyter notebook server, etc). These images can be hosted in an online repository such as `DockerHub <https://hub.docker.com/>`_. When needed, they can be easily downloaded and run on your host computer. When an image is run, it creates what is known as a Docker container that is an isolated and replicable instance of the operating system and your programs. You can then interact with the Docker container in a similar manner to how you would interact with a virtual machine e.g. mounting folders to access your files from the host system etc.

Contributors
============

- Thiranja Prasad Babarenda Gamage
- Chinchien Lin