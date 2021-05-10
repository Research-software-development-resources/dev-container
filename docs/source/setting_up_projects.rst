Setting up your software project
================================

You can setup your existing software projects (or create new ones) using the development-environment container. As example, we will clone and existing python module from Github.

1. Follow the instructions to run a commandline terminal in the development-environment container.

2. Run the following command within the container:

  .. code-block:: bash

    cd ~/opt
    git clone https://github.com/PrasadBabarendaGamage/mesh-tools.git

  .. Note::

    If you are using a PowerShell on a Windows host operating system, copy these commands one line at a time.

3. If you would like this module accessible from the terminal or IDEs you can add the path to the module to the ``PYTHONPATH`` environmental variable. This is typically achieved by updating your ``~/.bashrc`` file as described in the terminal beginner tutorial.

  1. Add the following to your ``~/oc/opt/bashrc`` file (this can be achieved using a text editor on your host operating system).

    .. Warning::

      On Windows hosts, it is recommended to use a text editor that is compatible with linux files such as `Notepad++ <https://notepad-plus-plus.org/downloads>`_. This is because the default notepad or wordpad programs on Windows use carriage returns as end-of-line deliminators, which are are not properly recognised by linux.

    .. code-block:: bash

       export PYTHONPATH=/home/jovyan/work/mesh-tools:$PYTHONPATH

       export JUPYTER_PATH=/home/jovyan/work/mesh-tools:$JUPYTER_PATH

