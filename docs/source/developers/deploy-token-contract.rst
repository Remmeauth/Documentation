#####################
Deploy Token Contract
#####################

Step 1: Clone and Build Contracts
=================================

Pull the source

.. code-block:: console

    $ git clone https://github.com/Remmeauth/rem.contracts.git && cd rem.contracts/contracts/rem.token

Compile ``rem.token`` contract

.. code-block:: console

    $ eosio-cpp -I include -o rem.token.wasm src/rem.token.cpp --abigen

.. note::
    In order to compile all the contracts, run the following script:

    .. code-block:: console

        $ ./build.sh

    This will save the compiled contracts in a ``build`` folder.

Step 2: Create Account for Contract
===================================

.. note::
    To create an account on a ``Local Testnet``, a ``development key`` must already be imported in your wallet.
    You can learn how to do this `here <development-wallet-configuration.html#step-6-import-the-development-key>`_.

Crete ``rem.token`` account

.. code-block:: console

    $ remcli create account rem rem.token rem@active

Step 3: Deploy Contract
=======================

.. code-block:: console

    $ remcli set contract rem.token ABSOLUTE_CONTRACT_DIR_PATH/rem.token -p rem.token@active

It will return something like:

.. code-block:: bash

    Publishing contract...
    executed transaction: b7cb62209325372d7fcd41b4fcd67fde995a5e8e53f7eddfa4de511d7f70d95f  7888 bytes  1080 us
    #           rem <= rem::setcode                 {"account":"rem.token","vmtype":0,"vmversion":0,"code":"0061736d0100000001ab011c60000060017e0060027f...
    #           rem <= rem::setabi                  {"account":"rem.token","abi":"0e656f73696f3a3a6162692f312e310008076163636f756e7400010762616c616e6365...
    warning: transaction executed locally, but may not be confirmed by the network yet         ]


Step 5: Create and Issue Tokens
===============================

To create a new token, call ``create`` action with the correct parameters.
``create`` action will accept 2 arguments:

- ``issuer`` - an account that has the right to issue or burning tokens. In our case, this ``alice``.
- ``maximum supply`` - this is the maximum amount that can be issued for a given symbol. In our case, this is ``SYS``.

.. code-block:: console

    $ remcli push action rem.token create '[ "alice", "1000000000.0000 SYS"]' -p rem.token@active

The command above created a new token ``SYS`` with a precision of 4 decimals and a maximum supply of ``1000000000.0000 SYS``.

.. code-block:: console

    executed transaction: be084a3024f13bf5ab17fb2254ec64522037eb2acf6fec458727b5db2a7a259b  120 bytes  402 us
    #     rem.token <= rem.token::create            {"issuer":"alice","maximum_supply":"1000000000.0000 SYS"}
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

To issue new tokens, call ``issue`` action.
Let's issue ``10000.0000 SYS`` tokens:

.. code-block:: console

    $ remcli push action rem.token issue '[ "alice", "1000.0000 SYS", "memo" ]' -p alice@active

It will return something like:

.. code-block:: bash

    executed transaction: 88424af9a20251cacacaf581695ee0afb6c3d523923bccea71c5c1449c135950  128 bytes  380 us
    #     rem.token <= rem.token::issue             {"to":"alice","quantity":"1000.0000 SYS","memo":"memo"}
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

Step 6: Transfer tokens
=======================

To transfer some tokens to bob, we use the ``transfer`` action:

.. code-block:: console

    $ remcli push action rem.token transfer '[ "alice", "bob", "500.0000 SYS", "memo" ]' -p alice@active

It will return something like:

.. code-block:: bash

    executed transaction: 2dc34f9a315c74a01059fbbd9a3fd1a3dff50b88c8a19b078777060968a9f731  136 bytes  279 us
    #     rem.token <= rem.token::transfer          {"from":"alice","to":"bob","quantity":"500.0000 SYS","memo":"memo"}
    #         alice <= rem.token::transfer          {"from":"alice","to":"bob","quantity":"500.0000 SYS","memo":"memo"}
    #           bob <= rem.token::transfer          {"from":"alice","to":"bob","quantity":"500.0000 SYS","memo":"memo"}
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

To check ``bob`` balance:

.. code-block:: console

    $ remcli get currency balance rem.token bob SYS

``bob`` balance is:

.. code-block:: bash

    500.0000 SYS




