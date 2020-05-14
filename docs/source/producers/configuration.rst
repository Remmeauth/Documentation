******************
Node Configuration
******************

Step 1: Download remchain settings
==================================
Get the genesis.json file that contains configuration of the REMChain network

.. code-block:: console

    $ wget https://remchain.remme.io/genesis.json

.. note::
    If you want to boot node on ``remchain testsnet`` use: https://testchain.remme.io/genesis.json

Step 2: Create configuration file
=================================
Create ``data`` and ``config`` folders.

.. code-block:: console

    $ mkdir data && mkdir config
    $ vim config/config.ini

Create ``config/config.ini`` and put the following settings into it:

.. code-block:: json

    plugin = eosio::chain_api_plugin
    plugin = eosio::net_api_plugin
    http-server-address = 0.0.0.0:8888
    p2p-listen-endpoint = 0.0.0.0:9876
    p2p-peer-address = p2p.remchain.remme.io:2087
    p2p-peer-address = Add someone else’s node here who you trust
    p2p-peer-address = Add someone else’s node here who you trust
    p2p-peer-address = Add someone else’s node here who you trust
    p2p-peer-address = Add someone else’s node here who you trust
    verbose-http-errors = true
    chain-state-db-size-mb = 100480
    reversible-blocks-db-size-mb = 10480

These config options should get you into the basic operation mode with your node API available at port ``8888``.
P2p-peer-address points to the other nodes where the new blocks are fetched from (you may specify multiple entries,
``p2p.remchain.remme.io:2087`` is the address of a node hosted by ``Remme``).

.. note::
    ``p2p-peer-address = Add someone else’s node here who you trust`` - this means you need to insert the address of
    the node that's up-to-date and which you trust.

Step 3: Create and Run Wallet
=============================

Firstly, you need to run wallet:

.. code-block:: console

    $ remvault &

You will see an output similar to the one below:

.. code-block:: console

   info  2018-11-26T06:54:24.789 thread-0  wallet_plugin.cpp:42          plugin_initialize    ] initializing wallet plugin
   info  2018-11-26T06:54:24.795 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/remvault/stop
   info  2018-11-26T06:54:24.796 thread-0  wallet_api_plugin.cpp:73      plugin_startup       ] starting wallet_api_plugin
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/create
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/create_key
   info  2018-11-26T06:54:24.796 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/wallet/get_public_key

Press enter to continue.

Than, you need to create ``default`` wallet:

.. code-block:: console

    $ remcli wallet create --file walletpass

To unlock your wallet use:

.. code-block:: console

    $ remcli wallet unlock < walletpass
