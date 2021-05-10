Installing additional python modules
====================================

You can install any python modules you wish to use with the development-environment container. As example, we will install the python ``scipy`` python package, and the ``h5py`` package that provides support for loading and saving files in hdf5 format.

1. Follow the instructions to run a commandline terminal in the development-environment container.

2. Run the following command within the container:

  .. code-block:: bash

    /opt/conda/bin/pip install --user h5py scipy

  .. Important::

    Do not forget to include the ``--user`` flag. This installs the module in the ``~/.local`` folder within the Docker container, which is mapped to `development-environment/usr/local/` folder on the host operating system. If this flag is not used, then the module will be installed in a system folder within the container, which will get erased when the container is shutdown.

.. Important::

  If you are using the JupyterLab IDE within the container, once new packages are installed, to use them, the JupyterLab kernel needs to be restarted. This can be achieved by selecting :guilabel:`Kernel` on JupyterLab and selecting :guilabel:`Restart Kernel`.