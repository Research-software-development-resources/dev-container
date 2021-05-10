Tunnelling into a docker container using ssh
============================================

Setup the SSH server
--------------------

1. Follow the instructions to run a commandline terminal in the development-environment container.

2. Run the following command within the container:

  .. code-block:: bash

    sudo start-ssh-server.sh

  This will enable remote access to the  docker container from your host machine through ssh tunnelling.

  .. Important::

    Running the script above, changes the password of the default user of the docker container (jovyan) to 'admin'.

SSH tunnelling into the running container
-----------------------------------------

From a terminal or PowerShell on your host machine, enter the following:

.. code-block:: bash

  ssh jovyan@localhost -p 10001

This will allow you to tunnel into the running container. 