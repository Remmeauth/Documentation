*******************
Install Remprotocol
*******************

Install binaries
================

Ubuntu 16.04/18.04
------------------
.. code-block:: console

    $ wget https://github.com/Remmeauth/remprotocol/releases/download/0.4.1/remprotocol_0.4.1.amd64.deb
    $ sudo apt install ./remprotocol_0.4.1.amd64.deb

CentOS
------
.. code-block:: console

    $ wget https://github.com/Remmeauth/remprotocol/releases/download/0.4.1/remprotocol_0.4.1.el7.x86_64.rpm
    $ sudo apt install ./remprotocol_0.4.1.el7.x86_64.rpm

Fedora
------
.. code-block:: console

    $ wget https://github.com/Remmeauth/remprotocol/releases/download/0.4.1/remprotocol_0.4.1.el7.x86_64.rpm
    $ sudo dnf install ./remprotocol_0.4.1.el7.x86_64.rpm

MacOs
-----
.. code-block:: console

    $ brew tap Remmeauth/remprotocol &&
    $ brew install remprotocol

.. note::
    To install the latest version, go to `Remprotocol releases <https://github.com/Remmeauth/remprotocol/releases/>`_.

Install from source
===================

Step 1: Download Remprotocol Source
-----------------------------------
.. code-block:: console

    $ git clone https://github.com/Remmeauth/remprotocol.git --recursive && cd remprotocol

Step 2: Build Remprotocol
-------------------------

To start build use:

.. code-block:: console

    $ ./scripts/eosio_build.sh -y

.. warning::
    The build process may take a long time. To start the build process in the background you can use ``nohup``:

    .. code-block:: console

        $ nohup ./scripts/eosio_build.sh -y > build.log &

    The build process logs will be saved in ``build.log``.

.. note::
    Script will be save binaries files in ``~/eosio/REM_VERSION/bin/``.
    To use ``remcli``, ``remvault``, ``remnode`` you should enter them to this directory and run them from here or
    you can add alias to bashrc.

.. tip::
    Aliases to use ``remcli``, ``remvault``, ``remnode`` from any directory:

    .. code-block:: json

        alias remcli='~/eosio/REM_VERSION/bin/remcli'
        alias remvault='~/eosio/REM_VERSION/bin/remvault'
        alias remnode='~/eosio/REM_VERSION/bin/remnode'

Add aliases to bashrc:
----------------------
.. code-block:: console

    $ echo "alias remcli='~/eosio/REM_VERSION/bin/remcli'\nalias remvault='~/eosio/REM_VERSION/bin/remvault'\nalias remnode='~/eosio/REM_VERSION/bin/remnode'" >> ~/.bashrc1

.. note::
    ``REM_VERSION`` - check version of the built Remprotocol in the ``~/eosio/`` directory.
    Replace the commands above ``REM_VERSION`` with your remprotocol version.

Step 3: Install Remprotocol
---------------------------
.. code-block:: console

    $ ./scripts/eosio_install.sh

