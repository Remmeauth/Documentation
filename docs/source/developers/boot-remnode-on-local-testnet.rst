#############################
Boot remnode on local testnet
#############################

Step 1: Start remvault
======================

.. code-block:: console

    $ remvault &

It will return something like:

.. code-block:: console

    info  2020-03-24T13:39:53.916 remvault  wallet_plugin.cpp:38          plugin_initialize    ] initializing wallet plugin
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/node/get_supported_apis
    info  2020-03-24T13:39:53.917 remvault  wallet_api_plugin.cpp:69      plugin_startup       ] starting wallet_api_plugin
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/create
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/create_key
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/get_public_keys
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/import_key
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/list_keys
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/list_wallets
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/lock
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/lock_all
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/open
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/remove_key
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/set_timeout
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/sign_digest
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/sign_transaction
    info  2020-03-24T13:39:53.917 remvault  http_plugin.cpp:699           add_handler          ] add api url: /v1/wallet/unlock

Press enter to continue

Troubleshooting
---------------

Command ``remvault`` should return something like:

.. code-block:: console

    Failed to lock access to wallet directory; is another remvault running?
    {}
    remvault  wallet_manager.cpp:304 initialize_lock

This is because another instance of ``remvault`` process might be running in the background.
To fix it run the following command ``pkill remvault`` and try again ``remvault``.

Step 2: Start remnode
=====================
.. note::
    For running local testnet, make sure that you've already imported to your wallet ``development key``.
    To learn how to configure the wallet see
    `here <development-wallet-configuration.html#step-6-import-the-development-key>`_.

.. code-block:: console

    $ remnode -e -p rem \
    --plugin eosio::producer_plugin \
    --plugin eosio::producer_api_plugin \
    --plugin eosio::chain_api_plugin \
    --plugin eosio::http_plugin \
    --plugin eosio::history_plugin \
    --plugin eosio::history_api_plugin \
    --filter-on="*" \
    --access-control-allow-origin='*' \
    --contracts-console \
    --http-validate-host=false \
    --verbose-http-errors >> remnode.log 2>&1 &

.. warning::
    In the above configuration, CORS is enabled * for development purposes only, you should never enable CORS *
    on a node that is publicly accessible!

.. note::
    Error ``Database dirty flag set (likely due to unclean shutdown): replay required`` talks that needs to replay
    database blockchain, add flag ``--replay-blockchain`` and try again.

Step 3: Make sure, that remnode is producing blocks
===================================================

.. code-block:: console

    $ tail -f remnode.log

Command ``tail`` should return something like:

.. code-block:: console

    info  2020-03-24T14:13:33.401 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block 77db3705466138a9... #8 @ 2020-03-24T14:13:33.500 signed by rem [trxs: 0, lib: 7, confirmed: 0]
    info  2020-03-24T14:13:33.901 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block a1f7a3672074bda2... #9 @ 2020-03-24T14:13:34.000 signed by rem [trxs: 0, lib: 8, confirmed: 0]
    info  2020-03-24T14:13:34.401 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block e4d3762538be3fff... #10 @ 2020-03-24T14:13:34.500 signed by rem [trxs: 0, lib: 9, confirmed: 0]
    info  2020-03-24T14:13:34.901 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block a8a2decdfd7f6dfb... #11 @ 2020-03-24T14:13:35.000 signed by rem [trxs: 0, lib: 10, confirmed: 0]
    info  2020-03-24T14:13:35.300 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block c2fca6f5e69eb06b... #12 @ 2020-03-24T14:13:35.500 signed by rem [trxs: 0, lib: 11, confirmed: 0]
    info  2020-03-24T14:13:35.901 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block 0f2792a1084733fb... #13 @ 2020-03-24T14:13:36.000 signed by rem [trxs: 0, lib: 12, confirmed: 0]
    info  2020-03-24T14:13:36.401 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block ee699d3dead21fcb... #14 @ 2020-03-24T14:13:36.500 signed by rem [trxs: 0, lib: 13, confirmed: 0]
    info  2020-03-24T14:13:36.901 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block 5b56d088f215d9b4... #15 @ 2020-03-24T14:13:37.000 signed by rem [trxs: 0, lib: 14, confirmed: 0]
    info  2020-03-24T14:13:37.400 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block ecdce8e2aecebfc3... #16 @ 2020-03-24T14:13:37.500 signed by rem [trxs: 0, lib: 15, confirmed: 0]
    info  2020-03-24T14:13:37.900 remnode   producer_plugin.cpp:2052      produce_block        ] Produced block 19240c4203ced119... #17 @ 2020-03-24T14:13:38.000 signed by rem [trxs: 0, lib: 16, confirmed: 0]



