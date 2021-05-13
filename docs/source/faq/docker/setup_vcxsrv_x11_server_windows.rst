Setup VcXsrv X11 server on Windows
==================================

.. _Setup VcXsrv X11 server on Windows:

The VcXsrv X11 server will be used to allow us visualise GUI programs, which are running inside the Docker container, on the host Windows machine. The following guide has been adapted from [this](https://dev.to/darksmile92/run-gui-app-in-linux-docker-container-on-windows-host-4kde) link.

1. Download VcXsrv from its `SourceForge repository <https://sourceforge.net/projects/vcxsrv/>`_.

2. Install VcXsrv with default options.

3. Run Xlaunch which gets installed by VcXsrv, and perform the initial configuration as follows:
    1. Display setting: select :guilabel:`multiple windows` option, and click :guilabel:`Next`.
    2. Client startup: check the :guilabel:`Start no client` option, and click :guilabel:`Next`.
    3. Extra setting: In addition to the default options, make sure "Disable access control" is enabled, and click :guilabel:`Next`.
    4. Click :guilabel:`Finish`.
