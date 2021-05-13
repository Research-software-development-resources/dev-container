Running PyCharm
===============

The following instructions describe how to run the PyCharm IDE using Docker or Singularity.

Starting the container
----------------------

Windows with Docker
~~~~~~~~~~~~~~~~~~~

1. Follow the instructions in the FAQ Docker 'Setup VcXsrv X11 server on Windows' Section.

  .. important::

    Ensure you have followed step 4 of the VcXsrv setup instructions. This step saves the IP address of your computer as an environmental variable in a PowerShell terminal. This specific step is required to be repeated each time you run PyCharm via docker.

2. Run the following command in a PowerShell (don't use a standard terminal, as it does not support commands that span multiple lines):

  .. code-block:: bash

    docker run `
        --rm `
        --env DISPLAY=${env:IPAddress}:0.0 `
        --name development-environment `
        -it `
        -v c/Users/${env:UserName}/Documents/development-environment/work:/home/jovyan/work `
        -v c/Users/${env:UserName}/Documents/development-environment/usr/local:/home/jovyan/.local `
        -v c/Users/${env:UserName}/Documents/development-environment/usr/cache:/home/jovyan/.cache `
        -v c/Users/${env:UserName}/Documents/development-environment/usr/config:/home/jovyan/.config `
        -v c/Users/${env:UserName}/Documents/development-environment/usr/java:/home/jovyan/.java `
        -v c/Users/${env:UserName}/Documents/development-environment/usr/bin/:/usr/local/bin/ `
        researchdevresources/development-environment:1.0-tensorflow-notebook start-pycharm.sh

  .. important::
    Ensure that there are no trailing spaces following the end-of-line tilda deliminators.

Linux or Mac with Docker
~~~~~~~~~~~~~~~~~~~~~~~~

When the commands below are executed, PyCharm will automatically be downloaded and installed in the ``~/work/PyCharm`` folder, which is a folder on the host machine that is mounted within the Docker container. This means that PyCharm will only need to be installed once and all settings will persist even after the Docker container is shutdown/restarted. The specific version of PyCharm that is downloaded can be specified in the ``development-environment/usr/bin/start-pycharm.sh`` script. By default, PyCharm 2020.2.3 is installed.

.. important::

  Repeat the ``docker run`` command if you receive an error like: 'docker: Error response from daemon'.

1. If you are running on Mac, follow the instructions in the FAQ Docker 'Setup XQuartz X11 server on Mac' Section.
2. Open a new terminal on your host machine.
3. Check that you are using the bash shell:

  .. code-block:: bash

    echo $SHELL

4. If the command above does not print ``/bin/bash`` then start a bash shell:

  .. code-block:: bash

    bash

5. If running on Linux, run the following:

  .. code-block:: bash

    docker run \
        --rm \
        --name development-environment \
        -e DISPLAY=${DISPLAY} \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        -v ~/development-environment/work:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/config:/home/jovyan/.config \
        -v ~/development-environment/usr/java:/home/jovyan/.java \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook start-pycharm.sh

  If running on Mac, run the following:

  .. code-block:: bash

    docker run \
        --rm \
        --name development-environment \
        -e DISPLAY=$IP:0 \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        -v ~/development-environment/work:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/config:/home/jovyan/.config \
        -v ~/development-environment/usr/java:/home/jovyan/.java \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook start-pycharm.sh

  .. important::

    Ensure that there are no trailing spaces following the end of line backslash deliminators.

Configuring PyCharm
-------------------
On the first run, you will need to configuring your python environment. 

1. Create a new project folder and store it in the ``/home/jovyan/work/`` folder.

2. In the interpreter section, select the existing system interpreter option and add the following path to the python interpreter:

  .. code-block:: bash

    /opt/conda/bin/python

3. Create the project.

Since the PyCharm and its settings are stored in a folder that is mapped to your host operating system, you will not need to repeat this setup next time you run the container.

.. seealso::
  Go to the tips Section in the local IDE page If you are running a Docker container following the instructions below. If you are running a Singularity container then skip this information.
