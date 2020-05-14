################################
Create Accounts on Local Testnet
################################

An account is an entity in the blockchain that contains basic information for direct interaction with the network
(changing the state of the network by receiving and sending transactions to the network).
Any account on the blockchain can be a smart contract.

Step 1: Create Test Accounts
============================

.. note::
    To create an account on a ``Local Testnet``, a ``development key`` must already be imported in your wallet.
    You can learn how to do this `here <development-wallet-configuration.html#step-6-import-the-development-key>`_.

To create test accounts use the following commands:

.. code-block:: console

    $ remcli create account rem alice PUBLIC_KEY
    $ remcli create account rem bob PUBLIC_KEY

This will return something like:

.. code-block:: console

    executed transaction: 245f82b202597593dd25b062e29bbfafd4eed842c43f0f3d69e8d0f3126c4711  200 bytes  423 us
    #           rem <= rem::newaccount              {"creator":"rem","name":"alice","owner":{"threshold":1,"keys":[{"key":"EOS6MRyAjQq8ud7hVNYcfnVPJqcVp...
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

.. note::
    ``PUBLIC_KEY`` - its a your public key that you already generate.
    If you did not generate a key go back to section
    `Development Wallet Configuration <development-wallet-configuration.html>`_.
    Replace ``PUBLIC_KEY`` to the yous public key.

The basic account creation interface for ``remcli`` looks like this:

.. code-block:: console

    Create a new account on the blockchain (assumes system contract does not restrict RAM usage)
    Usage: remcli create account [OPTIONS] creator name OwnerKey [ActiveKey]

    Positionals:
      creator TEXT                The name of the account creating the new account (required)
      name TEXT                   The name of the new account (required)
      OwnerKey TEXT               The owner public key or permission level for the new account (required)
      ActiveKey TEXT              The active public key or permission level for the new account

    Options:
      -h,--help                   Print this help message and exit
      -x,--expiration             set the time in seconds before a transaction expires, defaults to 30s
      -f,--force-unique           force the transaction to be unique. this will consume extra bandwidth and remove any protections against accidently issuing the same transaction multiple times
      -s,--skip-sign              Specify if unlocked wallet keys should be used to sign transaction
      -j,--json                   print result as json
      --json-file TEXT            save result in json format into a file
      -d,--dont-broadcast         don't broadcast transaction to the network (just print to stdout)
      --return-packed             used in conjunction with --dont-broadcast to get the packed transaction
      -r,--ref-block TEXT         set the reference block num or block id used for TAPOS (Transaction as Proof-of-Stake)
      --use-old-rpc               use old RPC push_transaction, rather than new RPC send_transaction
      -p,--permission TEXT ...    An account and permission level to authorize, as in 'account@permission' (defaults to 'creator@active')
      --max-cpu-usage-ms UINT     set an upper limit on the milliseconds of cpu usage budget, for the execution of the transaction (defaults to 0 which means no limit)
      --max-net-usage UINT        set an upper limit on the net usage budget, in bytes, for the transaction (defaults to 0 which means no limit)
      --delay-sec UINT            set the delay_sec seconds, defaults to 0s

Step 2: Get Test account
========================
Any ``Remprotocol`` Account contains the ``public keys`` linked to specific authorizations.
Flexible control of authorizations using account permissions allows you to divide account control
between certain actions for a group of people.

There are two basic types of permissions in ``Remprotocol``:

- ``owner`` - primary permission with full control over your account allowing you to change/add other permissions and all other basic actions.

- ``active`` - secondary permission with basic control over your account allowing you to send/receive transactions.

.. warning::
    For security reasons, use different keys for ``Active/Owner`` on a ``PRODUCTION`` Network.

.. code-block:: console

    $ remcli get account alice

It will return something like:

.. code-block:: console

    permissions:
     owner     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
        active     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    memory:
         quota:       unlimited  used:      2.66 KiB

    net bandwidth:
         used:               unlimited
         available:          unlimited
         limit:              unlimited

    cpu bandwidth:
         used:               unlimited
         available:          unlimited
         limit:              unlimited


