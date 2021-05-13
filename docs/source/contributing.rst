==================
Contributing (TBC)
==================

This section describes how to contribute to this documentation.

References
----------
New references can be added in bibtext format to `source/references.bib`.

Please note that the reference keys should be in Snake case (stylized as snake_case) :cite:`snake_case`. This refers to the style of writing in which each space is replaced by an underscore (_) character, and the first letter of each word written in lowercase.

The publication year (if any) should be appended to the reference key.

For example:

.. code-block:: bash

  @Book{1987_nelson,
    author = {Edward Nelson},
    title = {Radically Elementary Probability Theory},
    publisher = {Princeton University Press},
    year = {1987}
  }

Building and publishing Docker images to DockerHub
--------------------------------------------------
1. cd research-software-development-tutorials/docs/source/dockerfiles/developer-environment
2. docker build --tag development-environment:1.0-tensorflow-notebook .
3. docker tag development-environment:1.0-tensorflow-notebook researchdevresources/development-environment:1.0-tensorflow-notebook
4. docker login
5. docker push researchdevresources/development-environment:1.0-tensorflow-notebook


docker run --rm -it -e GRANT_SUDO=yes --user root researchdevresources/development-environment /bin/bash

.. bibliography:: refs.bib
  :style: alpha
