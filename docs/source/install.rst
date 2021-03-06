Installation
============

Directory setup
---------------

Before we install the development-environment, we will first create a set of folders within your host operating system. These folders will be mounted within the development-environment Docker container when it is run to allow you to access the files in these folders from within the container (much like how you would map/mount a drive on Windows, Mac, or Linux). The following commands for running development-environment Docker containers expect the following folder structure:

.. code-block:: bash

  development-environment
  └───work
  |       bashrc
  |
  └───usr
      |
      └───bin
      │       start.sh
      │       start-notebook.sh
      │       start-singleuser.sh
      │       start-ssh-server.sh
      |       start-pycharm.sh
      |       mount-shared-drive.sh
      │       fix-permissions
      |
      └───etc
      │   │
      │   └───jupyter
      │           jupyter_notebook_config.py
      │
      └───local
      │
      └───cache
      │
      └───java
      │
      └───config
      │
      └───PyCharm

This folder structure contains:

1. ``work`` - this will be your main working directory.
2. ``usr/bin`` - folder containing scripts for running different programs in the container e.g. jupyter servers etc.
3. ``usr/etc/jupyter`` - folder containing jupyter notebook configuration.
4. ``usr/local`` and ``usr/cache`` - folders where new python modules installed will be stored.
5. ``usr/java``, ``usr/config``, and ``usr/PyCharm`` - folders used by IDEs.

.. warning::

  The working development-environment/work directory created on the host machine will be mapped to `/home/jovyan/work` within the Docker container. Only items within folders that are mapped from the host operating system to the container will persist once the container is shutdown. Any files outside these folders will not be recoverable (running a Docker container can be thought of as getting a new computer with a fresh installation - only items in the mapped drive will be available the next time you start the Docker container).

This folder structure and its associated files have been stored in the following zip file (See :download:`zip file <_static/development-environment.zip>`). Simply extract the folder as described below:

Windows
~~~~~~~
1. Move the downloaded zip file to your ``Documents`` folder (this is typically located in ``C:/Users/USER_NAME/Documents/``, where USER_NAME is your Windows login name).

2. Extract the zip file into this folder.

3. Once extracted, the ``development-environment`` folder should be found in ``C:/Users/USER_NAME/Documents/development-environment``.

  .. important::
    Check the extracted folder to ensure that the zip file was extracted as ``C:/Users/USER_NAME/Documents/development-environment`` and not ``C:/Users/USER_NAME/Documents/development-environment/development-environment``.

.. important::
  If your ``Documents`` folder is hosted on e.g. Microsoft One Drive, then manually create the ``Documents`` folder specified in Step 1 above and follow the subsequent steps described above.

.. note::
  If you would like to have the directory structure stored in a different location e.g. on drive other than ``C:`` then:

  1. Open the files in the ``start_pycharm_from_windows.bat`` with a text editor such as Notepad++.
  2. Search for all occurrences of ``c/Users/%UserName%/Documents/`` and replace it with the path to where you want to store your directory structure.
  3. Continue from Step 2 above.

  .. note::

    Docker does not support mounting of network drives, so please select a physical drive to store your directory structure.

Linux and Mac
~~~~~~~~~~~~~
Go to your home directory and extract the zip file. For example, on linux `~` refers to `/home/$USER/`. Once extracted, the `development-environment` folder should be located in `/home/$USER/development-environment`.

.. code-block:: bash

  cd ~
  wget https://dev-container.readthedocs.io/en/latest/_static/development-environment.zip
  unzip development-environment.zip

Installing docker
-----------------

Now that the your directory structure has been setup, the next step is to install Docker Desktop.

Windows
~~~~~~~
1. Install `Docker Desktop <https://www.docker.com/products/docker-desktop>`_.
3. Restart your machine.

Linux
~~~~~
1. Follow instructions on `Docker's engine install documentation <https://docs.docker.com/engine/install>`_.

2. Follow the instructions on the *Manage Docker as a non-root user* section on `Docker's linux-post install documentation <https://docs.docker.com/engine/install/linux-postinstall>`_ to add your username to the docker group. This will enable you to run docker without requiring super user permission. This is important to ensure that all the files generated by the docker are owned by the user and not the root superuser.

3. Once installed, the docker service should already be running.

4. Change permissions on the ``development-environment`` folder that was downloaded in the previous section to allow read and write permissions for the docker group.

Mac
~~~
1. On Mac, install Docker Desktop for Mac (macOS) from docs.docker.com/engine/install/
2. Open the Docker Desktop For Mac app.








