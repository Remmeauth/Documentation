################
Preparation step
################

Step 1: Install dependency
==========================

Ubuntu 16.04/18.04
------------------
.. code-block:: console

    $ sudo apt-get update && sudo apt-get install build-essential cmake

CentOS
------
.. code-block:: console

    $ sudo yum update && sudo yum groupinstall "Development Tools" cmake

Fedora
------
.. code-block:: console

    $ sudo dnf update && sudo dnf groupinstall "Development Tools" cmake

MacOs
------
.. code-block:: console

    $ brew install cmake

Step 2: Install eosio.cdt
=========================

.. warning::
    If you have versions of eosio.cdt prior to 1.3.0 installed on your system, please uninstall before proceeding.

Ubuntu 16.04/18.04
------------------
.. code-block:: console

    $ wget https://github.com/eosio/eosio.cdt/releases/download/v1.7.0/eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb
    $ sudo apt install ./eosio.cdt_1.7.0-1-ubuntu-18.04_amd64.deb

CentOS
------
.. code-block:: console

    $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio-1.7.0-1.el7.x86_64.rpm &&
    $ sudo yum install ./eosio-1.7.0-1.el7.x86_64.rpm

Fedora
------
.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio-1.7.0-1.fc27.x86_64.rpm && \
   $ sudo yum install ./eosio-1.7.0-1.fc27.x86_64.rpm

MacOs
------
.. code-block:: console

    $ brew tap eosio/eosio.cdt
    $ brew install eosio.cdt

.. note::
    To install ``eosio.cdt`` from source you can read instructions
    `here <https://developers.eos.io/welcome/latest/getting-started/development-environment/install-the-CDT/#install-from-source>`_.
    Node should be configured with at least 2 CPUs (does not have to be two physical ones) and 8G of memory to avoid compilation errors.

Step 3: Install binaries
========================

.. note::
    To get started as quickly as possible we recommend using pre-built binaries. Building from source is a
    more advanced option but will set you back an hour or more and you may encounter build errors.

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
    - To install the latest version, go to `Remprotocol releases <https://github.com/Remmeauth/remprotocol/releases/>`_.

    - How to `build Remprotocol from source <../producers/install-remprotocol.html#install-from-source>`_.
