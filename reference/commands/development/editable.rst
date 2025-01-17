
.. _conan_editable:

conan editable
==============

.. code-block:: bash

    $ conan editable [-h] {add,remove,list} ...

Manages editable packages (packages that reside in the user workspace, but
are consumed as if they were in the cache).

Use the subcommands 'add', 'remove' and 'list' to create, remove or list
packages currently installed in this mode.

.. code-block:: text

    positional arguments:
      {add,remove,list}  sub-command help
        add              Put a package in editable mode
        remove           Disable editable mode for a package
        list             List packages in editable mode

    optional arguments:
      -h, --help         show this help message and exit


.. _conan_editable_add:

conan editable add
------------------

.. code-block:: bash

    $ conan editable add [-h] [-l LAYOUT] path reference

Opens the package ``<reference>`` in editable mode in the user folder ``<path>``

.. code-block:: text

    positional arguments:
    path                  Path to the package folder in the user workspace
    reference             Package reference e.g.: mylib/1.X@user/channel

    optional arguments:
    -h, --help            show this help message and exit
    -l LAYOUT, --layout LAYOUT
                            Relative or absolute path to a file containing the
                            layout. Relative paths will be resolved first relative
                            to current dir, then to local cache "layouts" folder
    -of OUTPUT_FOLDER, --output-folder OUTPUT_FOLDER
                        The root output folder for generated and build files
    -sf SOURCE_FOLDER, --source-folder SOURCE_FOLDER
                        The root source folder



This command puts a package in :ref:`"Editable mode" <editable_packages>`, and consumers of this package will use
it from the given user folder instead of using it from the cache.
The path pointed by ``path`` should exist and contain a ``conanfile.py``.

Example: Put the package ``cool/version@user/dev`` in editable mode, using the layout specified by
the file ``win_layout``.

.. code-block:: bash

    $ conan editable add . cool/version@user/dev --layout=win_layout


The ``--output-folder`` and ``--source-folder`` will specify the location of the output (build files, generators, etc)
and the source folders, with the same meaning as the ``conan install`` command.
By default, if not specified, they will point to the folder containing the ``conanfile.py``. These arguments work
together with the ``layout()`` method to determine the location of the different Conan and build files.



conan editable remove
---------------------

.. code-block:: bash

    $ conan editable remove [-h] reference

Removes the editable mode of package ``reference``.

.. code-block:: text

    positional arguments:
    reference   Package reference e.g.: mylib/1.X@user/channel

    optional arguments:
    -h, --help  show this help message and exit


Example: remove the "Editable mode", use again package from the cache:

.. code-block:: bash

    $ conan editable remove cool/version@user/dev


conan editable list
-------------------

.. code-block:: bash

    $ conan editable list [-h]

Shows the list of the packages that are opened in "editable" mode.
