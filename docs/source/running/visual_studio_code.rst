Running Visual Studio Code
==========================

The following instructions describe how to run the Visual Studio Code IDE using Docker or Singularity.

Starting the container
----------------------

When the commands below are executed, Visual Studio Code will automatically be downloaded and installed in the ``~/opt/VSCode-linux-x64`` folder, which is a folder on the host machine that is mounted within the Docker container. This means that Visual Studio Code will only need to be installed once and all settings will persist even after the Docker container is shutdown/restarted. The specific version of Visual Studio Code that is downloaded can be specified in the ``development-environment/usr/bin/start-vs-code.sh`` script. By default, Visual Studio Code 1.51.1 is installed.

.. important::

  Repeat the ``docker run`` command if you receive an error like: 'docker: Error response from daemon'.

Linux or Mac with Docker
~~~~~~~~~~~~~~~~~~~~~~~~

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
        -v ~/development-environment/opt:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook start-vs-code.sh

  If running on Mac, run the following:

  .. code-block:: bash

    docker run \
        --rm \
        --name development-environment \
        -e DISPLAY=$IP:0 \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        -v ~/development-environment/opt:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/config:/home/jovyan/.config \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook start-vs-code.sh

  .. important::

    Ensure that there are no trailing spaces following the end of line backslash deliminators.

Windows with Docker
~~~~~~~~~~~~~~~~~~~
Running the Visual Studio Code IDE in a docker on a Windows host is not supported at this time. See the following `github issue <https://github.com/OpenCMISS-Examples/OpenCMISS-Iron-tutorials/issues/8>`_ for more information.