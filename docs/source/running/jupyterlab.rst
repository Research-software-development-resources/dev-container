Running JupyterLab
==================

The following instructions describe how to run the JupyterLab IDE using Docker or Singularity.

Starting the container
----------------------

.. important::

  Repeat the ``docker run`` command if you receive an error like: 'docker: Error response from daemon'.

Linux or Mac with Docker
~~~~~~~~~~~~~~~~~~~~~~~~

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
        -p 10000:8888 \
        -e JUPYTER_ENABLE_LAB=yes \
        -v ~/development-environment/work:/home/jovyan/work \
        -v ~/development-environment/usr/local:/home/jovyan/.local \
        -v ~/development-environment/usr/cache:/home/jovyan/.cache \
        -v ~/development-environment/usr/etc/jupyter:/etc/jupyter \
        -v ~/development-environment/usr/bin/:/usr/local/bin \
        researchdevresources/development-environment:1.0-tensorflow-notebook

  .. important::

    Ensure that there are no trailing spaces following the end of line backslash deliminators.


Linux with Singularity
~~~~~~~~~~~~~~~~~~~~~~

Repeat steps 1-3 above and then run the following:

.. code-block:: bash

  SINGULARITY_JUPYTER_ENABLE_LAB=yes singularity run \
      -B ~/development-environment/work:/home/jovyan/work \
      -B ~/development-environment/usr/local:/home/jovyan/.local \
      -B ~/development-environment/usr/cache:/home/jovyan/.cache \
      -B ~/development-environment/usr/etc/jupyter:/etc/jupyter \
      -B ~/development-environment/usr/bin/:/usr/local/bin \
      docker://researchdevresources/development-environment:1.0-tensorflow-notebook

.. important::

  Ensure that there are no trailing spaces following the end of line backslash deliminators.

Windows with Docker
~~~~~~~~~~~~~~~~~~~
Run the following command in a PowerShell (don't use a standard terminal, as it does not support commands that span multiple lines):

.. code-block:: bash

  docker run `
      --rm `
      --name development-environment `
      -p 10000:8888 `
      -e JUPYTER_ENABLE_LAB=yes `
      -v c/Users/${env:UserName}/Documents/development-environment/work:/home/jovyan/work `
      -v c/Users/${env:UserName}/Documents/development-environment/usr/local:/home/jovyan/.local `
      -v c/Users/${env:UserName}/Documents/development-environment/usr/cache:/home/jovyan/.cache `
      -v c/Users/${env:UserName}/Documents/development-environment/usr/etc/jupyter:/etc/jupyter `
      -v c/Users/${env:UserName}/Documents/development-environment/usr/bin/:/usr/local/bin/ `
      researchdevresources/development-environment:1.0-tensorflow-notebook

.. important::
  Ensure that there are no trailing spaces following the end-of-line tilda deliminators.


Accessing JupyterLab
--------------------
The above commands will start a JupyterLab server on port ``8888`` within the docker container.

A JupyterLab interactive session can be started in the browser of your host machine by copying and pasting the url with the access token (highlighted in yellow in the figure below) into a web browser (e.g. chrome). 

  .. figure:: docker_jupyter_server_url.png
    :width: 700
    :class: with-shadow
    :figclass: align-center

    Docker JupyterLab server url.

.. important::
  If you are running a Docker container following the instructions below. If you are running a Singularity container then skip this information.

  Note that the above url will give a ``This site can’t be reached 127.0.0.1 refused to connect`` error. This is because the `docker run` command above maps port number ``8888`` within the container to port number ``10000`` on the host windows machine. Replace ``8888`` with ``10000`` in the url and the JupyterLab interactive session will load as expected in your web browser.

  Singularity does not require mapping of ports.

Working with JupyterLab
-----------------------

See the IDE page for more information on how to use JupyterLab.

