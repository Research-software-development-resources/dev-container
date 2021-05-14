Running PyCharm
===============

The following instructions describe how to run the PyCharm IDE using Docker or Singularity.

Starting the container
----------------------

Windows with Docker
~~~~~~~~~~~~~~~~~~~

1. Follow the instructions in :ref:`Setup VcXsrv X11 server on Windows` in the FAQ Docker section.

2. Open the ``C:/Users/USER_NAME/Documents/development-environment/shortcuts`` folder (or where you have extracted the ``development-environment`` folder).

3. Double click on the ``start_pycharm_from_windows.bat`` file to run the container.

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

On the first run, you will need to configuring your python environment. This involves selecting the Anaconda python 3.9 interpreter that has been setup within the container.

.. warning::

  Only use the Anaconda Python 3.9 interpreter as shown below for building your software projects within the container and not the system default in ``/usr/bin/python3.8``. This is because only changes to the Anaconda Python 3.9 interpreter (e.g. installation of new libraries) will persist when the container is shutdown.

.. note::

  Since the PyCharm and its settings are stored in a folder that is mapped to your host operating system, you will not need to repeat this setup next time you run the container.


New projects
~~~~~~~~~~~~

1. Create a new project folder and store it in the ``/home/jovyan/work/`` folder. e.g. ``/home/jovyan/work/my_new_project``

  .. important::

    This is important because only files/folders within ``/home/jovyan/work/`` are mapped to the host operating systems. Files outside of this folder will be lost when the container is shutdown.

2. Select the Anaconda Python 3.9 interpreter that has been setup in the container:

  1. In the :guilabel:`Python interpreter section`, select :guilabel:`Previously configured interpreter`.

  2. Click the three dots next to the :guilabel:`interpreter` option.

    .. figure:: pycharm_path_to_interpreter.png
      :width: 600
      :class: with-shadow
      :figclass: align-center

      Select path to python interpreter in PyCharm.

  3. Specify the following path for the python interpreter:

    .. code-block:: bash

      /opt/conda/bin/python

  4. Create the project.

Existing projects
~~~~~~~~~~~~~~~~~

1. On your host operating system, move or clone your project into the ``development-environment/work/`` folder. e.g. ``development-environment/work/my_existing_project``. This folder will be available within the container in ``/home/jovyan/work/my_existing_project``.

2. Upon running PyCharm from the container, select :guilabel:`Open` on the PyCharm landing page (or :guilabel:`File` → :guilabel:`Open`) and select your project folder e.g. ``/home/jovyan/work/my_existing_project``.

3. Select the Anaconda Python 3.9 interpreter that has been setup in the container:

  1. Select :guilabel:`File` → :guilabel:`Settings`.

  2. Select :guilabel:`Project: my_existing_project` → :guilabel:`Python Interpreter`.

  3. Click the gear icon → :guilabel:`Add` on the top right of the settings window.

  4. Perform step 2 onwards from the previous ``New projects`` section.

Enabling automatic saving of open files in PyCharm
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Enable automatic saving of open files by following the tips suggested in the PyCharm tips section of the `research-software-development-tutorials <https://research-software-development-tutorials.readthedocs.io/en/latest/beginner/development_environments/ides.html#pycharm-tips>`_.


