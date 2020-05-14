################
Preparation step
################

Disclaimer
==========
There are a variety of tools which require you to have basic knowledge on how to use them in the terminal.

Step 1: Install dependencies
============================

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


Step 2: install eosio.cdt:
==========================

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
