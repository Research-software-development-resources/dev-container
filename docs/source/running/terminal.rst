Running a command line terminal
===============================

Starting the container
----------------------

Start a command line terminal within the development-environment Docker container by executing the following commands (ensure that there are no trailing spaces following the end-of-line deliminators):

.. important::

  Repeat the `docker run` command if you receive an error like: 'docker: Error response from daemon'.

Linux and Mac
~~~~~~~~~~~~~
1. Open a new terminal on your host machine.
2. Check that you are using the bash shell:

  .. code-block:: bash

    echo $SHELL

3. If the command above does not print ``/bin/bash`` then start a bash shell:

  .. code-block:: bash

    bash

4. Run the following:

  .. code-block:: bash

    docker run \
        --rm \
        --name development-environment \
        -it \
        -v ~/development-environment/work:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/etc/jupyter:/etc/jupyter \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook start-terminal.sh

  .. important::

    Ensure that there are no trailing spaces following the end of line backslash deliminators.

Windows
~~~~~~~

1. Open a new PowerShell on your host machine (don't use a standard terminal, as it does not support commands that span multiple lines).
2. Run the following:       

  .. code-block:: bash

docker run `
    --rm `
    --name development-environment `
    -it `
    -v c/Users/${env:UserName}/Documents/development-environment/work:/home/jovyan/work `
    -v c/Users/${env:UserName}/Documents/development-environment/usr/local:/home/jovyan/.local `
    -v c/Users/${env:UserName}/Documents/development-environment/usr/cache:/home/jovyan/.cache `
    -v c/Users/${env:UserName}/Documents/development-environment/usr/etc/jupyter:/etc/jupyter `
    -v c/Users/${env:UserName}/Documents/development-environment/usr/bin/:/usr/local/bin/ `
    researchdevresources/development-environment:1.0-tensorflow-notebook start.sh

  .. important::
    Ensure that there are no trailing spaces following the end-of-line tilda deliminators.

Running python scripts
----------------------
The command in the previous section will open a new bash terminal within the running development-environment Docker container as shown below:

  .. figure:: docker_start_bash_terminal.png
    :width: 700
    :class: with-shadow
    :figclass: align-center

    A bash terminal running within the development-environment container.

In this terminal, either:

1. run python from the terminal: 

  .. code-block:: bash

    python

2. or run a python script directly from the terminal:

  .. code-block:: bash

    python your_python_script.py

  .. note::

    As your ``work`` folder on your host operating system is mapped to ``/home/jovyan/work`` within the container, you can place python scripts in this folder and run them from within the container.

    .. code-block:: bash

      python /home/jovyan/work/your_python_script.py

    or

    .. code-block:: bash

      cd /home/jovyan/work
      python your_python_script.py

Docker run commandline arguments (optional information)
-------------------------------------------------------

The commandline arguments associated with the ``docker run`` command are listed below:

- ``--name development-environment`` This argument specifies the name of the container that the ``docker run`` command will create.
- ``-it`` Run the docker container in an interactive mode. This will allow us to open a terminal within the development-environment container to perform some additional setup steps.
- ``-v [host-src]:[container-dest]`` Allows a folder, ``[host-src]``, on the host operating system (such as our environment folder described in the previous step, to be mounted within the container in the location specified by ``[container-dest]``. For example,  e.g. ``-v ~/development-environment/work:/home/jovyan/work`` will mount a folder located at ``~/development-environment/work`` on the host operating system to ``/home/jovyan/work`` in the container).
- The final argument that the ``docker run`` command requires is the name of the script to run within the the container when it starts up. The OpenCMISS-Docker image has been automatically configured to access scripts located in the ``development-environment/usr/bin`` folder folder without needing to specify their full path.
- The second to last argument of the ``docker run`` command indicates the location of the Docker image that you want to run e.g. ``researchdevresources/development-environment:1.0`` points to a image hosted on DockerHub.

More information on arguments for the ``docker run`` command can be found in `Docker engine reference documentation <https://docs.docker.com/engine/reference/run>`_.


