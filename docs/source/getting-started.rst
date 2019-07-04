***************
Getting Started
***************

Disclaimer
==========

There are a variety of tools which require to have basic knowledge on how to use them in the terminal.

Step 1: install binaries
========================

If you have previous versions of ``Remme protocol`` installed on your machine, please uninstall before proceeding.
Detailed instructions are below.

MacOS
-----

.. code-block:: console

   $ brew tap eosio/eosio && \
         brew install eosio

Ubuntu 18.04
------------

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio_1.7.0-1-ubuntu-18.04_amd64.deb && \
         sudo apt install ./eosio_1.7.0-1-ubuntu-18.04_amd64.deb

Ubuntu 16.04
------------

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio_1.7.0-1-ubuntu-16.04_amd64.deb && \
         sudo apt install ./eosio_1.7.0-1-ubuntu-16.04_amd64.deb

CentOS
------

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio-1.7.0-1.el7.x86_64.rpm && \
         sudo yum install ./eosio-1.7.0-1.el7.x86_64.rpm

Fedora
------

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio-1.7.0-1.fc27.x86_64.rpm && \
         sudo yum install ./eosio-1.7.0-1.fc27.x86_64.rpm

Step 2: boot node and wallet
============================

Start keosd
-----------

Start ``keosd``:

.. code-block:: console

   $ keosd &

You will see an output similar to the one below:

.. code-block:: console

   info  2018-11-26T06:54:24.789 thread-0  wallet_plugin.cpp:42          plugin_initialize    ] initializing wallet plugin
   info  2018-11-26T06:54:24.795 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/keosd/stop
   info  2018-11-26T06:54:24.796 thread-0  wallet_api_plugin.cpp:73      plugin_startup       ] starting wallet_api_plugin
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/create
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/create_key
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/get_public_key

Press enter to continue.

Start nodeos
------------

Start ``nodeos``. This command loads all the basic plugins, set the server address, enable |cors_reference_mozzila|
(with no restrictions and development logging) and add some contract debugging and logging.

.. |cors_reference_mozzila| raw:: html

   <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS" target="_blank">CORS</a>

.. code-block:: console

   $ nodeos -e -p eosio \
         --plugin eosio::producer_plugin \
         --plugin eosio::chain_api_plugin \
         --plugin eosio::http_plugin \
         --access-control-allow-origin='*' \
         --contracts-console \
         --http-validate-host=false \
         --verbose-http-errors >> nodeos.log 2>&1 &

.. note::

    In the above configuration, ``CORS`` is enabled for ``*`` for development purposes only, you should never enable
    ``CORS`` for ``*`` on a node that is publicly accessible!

Step 3: check that nodeos is producing blocks
=============================================

Run the following command:

.. code-block:: console

    tail -f nodeos.log

You will see an output similar to the one below:

.. code-block:: console

    1929001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366974ce4e2a... #13929 @ 2018-05-23T16:32:09.000 signed by eosio [trxs: 0, lib: 13928, confirmed: 0]
    1929502ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366aea085023... #13930 @ 2018-05-23T16:32:09.500 signed by eosio [trxs: 0, lib: 13929, confirmed: 0]
    1930002ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366b7f074fdd... #13931 @ 2018-05-23T16:32:10.000 signed by eosio [trxs: 0, lib: 13930, confirmed: 0]
    1930501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366cd8222adb... #13932 @ 2018-05-23T16:32:10.500 signed by eosio [trxs: 0, lib: 13931, confirmed: 0]
    1931002ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366d5c1ec38d... #13933 @ 2018-05-23T16:32:11.000 signed by eosio [trxs: 0, lib: 13932, confirmed: 0]
    1931501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366e45c1f235... #13934 @ 2018-05-23T16:32:11.500 signed by eosio [trxs: 0, lib: 13933, confirmed: 0]
    1932001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366f98adb324... #13935 @ 2018-05-23T16:32:12.000 signed by eosio [trxs: 0, lib: 13934, confirmed: 0]
    1932501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 00003670a0f01daa... #13936 @ 2018-05-23T16:32:12.500 signed by eosio [trxs: 0, lib: 13935, confirmed: 0]
    1933001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 00003671e8b36e1e... #13937 @ 2018-05-23T16:32:13.000 signed by eosio [trxs: 0, lib: 13936, confirmed: 0]
    1933501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000367257fe1623... #13938 @ 2018-05-23T16:32:13.500 signed by eosio [trxs: 0, lib: 13937, confirmed: 0]

Press ``ctrl`` + ``c`` to close an output.

Step 3: check the wallet
========================

Run the following command, we need to validate the installation and check if wallet is working as intended:

.. code-block:: console

    $ cleos wallet list

You will see an output similar to the one below:

.. code-block:: console

    $ Wallets:
    []

Step 4: check nodeos endpoints
==============================

Run the following command, this will check that the ``RPC API`` is working correctly:

.. code-block:: console

   $ curl http://localhost:8888/v1/chain/get_info

Uninstall binaries
==================

MacOS
-----

.. code-block:: console

   $ brew remove eosio

Ubuntu
------

.. code-block:: console

   $ sudo apt remove eosio

CentOS
------

.. code-block:: console

   $ sudo yum remove eosio

Fedora
------

.. code-block:: console

   $ sudo yum remove eosio
