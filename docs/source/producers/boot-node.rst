*********
Boot Node
*********

Start remnode
=============

The first ``remnode`` run:

.. code-block:: console

    $ remnode --config-dir ./config/ --data-dir ./data/ --delete-all-blocks --genesis-json genesis.json

.. warning::
    It should start syncing blocks now. Wait until it downloads previous blocks and starts to receive current blocks.
    Press ``ctrl`` + ``с`` to stop it.

For subsequent runs of the ``remnode``, use:

.. code-block:: console

    $ remnode --config-dir ./config/ --data-dir ./data/ >> remnode.log 2>&1 &

.. note::
    The command above will run the ``remnode`` in the background and will save its output to the ``remnode.log`` file.
    If you want to stop the ``remnode`` that runs in the background, run this:

.. code-block:: console

    $  killall remnode

If your node is connected and synced, this command should return you the information about the chain:

.. code-block:: console

    $ remcli get info
      {
      "server_version": "72dadefc",
      "chain_id": "9f485317b61a19e956c822866cc57a64bbed2196e1cf178e80f847a139a20916",
      "head_block_num": 15757338,
      "last_irreversible_block_num": 15757006,
      "last_irreversible_block_id": "00f06ecebf0b87814c9f1c4d9b7acbe637e2e9ecf11a01a22baa62c6b112afb8",
      "head_block_id": "00f0701a1f7203a5a124c250aba48e9967383ca592cb84361c2856cc48f62a5e",
      "head_block_time": "2020-03-18T21:12:21.500",
      "head_block_producer": "remproduce43",
      "virtual_block_cpu_limit": 200000000,
      "virtual_block_net_limit": 1048576000,
      "block_cpu_limit": 200000,
      "block_net_limit": 1048576,
      "server_version_string": "v0.4.1",
      "fork_db_head_block_num": 15757338,
      "fork_db_head_block_id": "00f0701a1f7203a5a124c250aba48e9967383ca592cb84361c2856cc48f62a5e",
      "server_full_version_string": "v0.4.1-72dadefcf013ab65b0840c600dad2382fde7f8c2"
      }

``remcli`` (analog of cleos in EOSIO terms) is a command-line tool that has a rich variety of functions.
It has nearly everything that you may need to interact with the blockchain.
You may start getting familiar with it by running ``remcli --help``.
