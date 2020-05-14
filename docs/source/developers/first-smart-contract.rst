####################
First Smart Contract
####################

Write contract
==============

| We will write a contract that will validate the name on the ``Remchain`` and check whether such an account exists.

| First, create a directory for the contract.

.. code-block:: console

    $ mkdir name_validator
    $ cd name_validator

Create a source file ``name_validator.cpp`` and open in editor.

.. code-block:: console

    $ touch name_validator.cpp

In order to create a contract, you need to import ``eosio.hpp`` header file and extend the ``eosio::contract`` class.

.. code-block:: c++

    #include <eosio/eosio.hpp>

Next we will create an empty contract class.

.. code-block:: c

    #include <eosio/eosio.hpp>

    class [[eosio::contract]] name_validator : public eosio::contract {};

Add a public access specifier and a using-declaration. The ``using`` declaration will allow us to write more concise code.

.. code-block:: c

    #include <eosio/eosio.hpp>

    class [[eosio::contract]] name_validator : public eosio::contract {
      public:
          using contract::contract;
    };

The logic of the behavior of the contract determines the action. We will write an action that prints whether
such an account exists on the ``Remchain``.

.. note::
    | ``Action`` - Functionality exposed by a smart contract that is exercised by passing the correct parameters via an
     approved transaction to an EOSIO network.

    | Refer to EOSIO’s `glossary <https://developers.eos.io/welcome/latest/glossary/index#action>`_.

.. code-block:: c

    #include <eosio/eosio.hpp>

    class [[eosio::contract]] name_validator : public eosio::contract {
      public:
          using contract::contract;

          [[eosio::action]]
          void validatename( std::string username ) {
              eosio::name user{username};
              eosio::check( !eosio::is_account(user), "account already exists" );
    };

| EOSIO provides many useful types and methods for a contracts.
| Type `name <https://developers.eos.io/manuals/eosio.cdt/latest/structeosio_1_1name>`_ defines username in ``Remchain``.
| Function `check() <https://developers.eos.io/manuals/eosio.cdt/latest/namespaceeosio#function-check-16>`_
  is asserted if the predicate fails and uses the supplied message.
| Function `is_account() <https://developers.eos.io/manuals/eosio.cdt/latest/group__action/#function-is_account>`_
  verifies that ``user`` is an existing account, the return type is ``bool``.

.. note::
    The ABI ``<<glossary:ABI>>`` generator in ``eosio.cdt`` won't know about the ``isaccount()`` action without an
    attribute ``[[eosio::action]]``. The ABI Generator in ``eosio.cdt`` supports several different style of attributes,
    see the ABI usage guide on `EOSIO <https://developers.eos.io/welcome/latest/getting-started/smart-contract-development/understanding-ABI-files>`_.

Now, add ``check`` for validation name length:

.. code-block:: c

    #include <eosio/eosio.hpp>

    class [[eosio::contract]] name_validator : public eosio::contract {
      public:
          using contract::contract;

          [[eosio::action]]
          void validatename( std::string username ) {
              eosio::name user{username};
              eosio::check( !eosio::is_account(user), "account already exists" );
              eosio::check( user.length() == name_length, "account name must be 12 characters" );
          }
      private:
          uint8_t name_length = 12;
    };

.. note::
    After setting the contract, the following naming conventions:
        - Can only contain the characters ``.abcdefghijklmnopqrstuvwxyz12345``. ``a-z`` (lowercase), ``1-5`` and ``.`` (period)
        - Must start with a letter
        - Must be 12 characters

Using the ``eosio`` namespace will reduce clutter in your code, let's do that:

.. code-block:: c

    #include <eosio/eosio.hpp>

    using namespace eosio;

    class [[eosio::contract]] name_validator : public contract {
      public:
          using contract::contract;

          [[eosio::action]]
          void validatename( std::string username ) {
              name user{username};
              check( !is_account(user), "account already exists" );
              check( user.length() == name_length, "account name must be 12 characters" );
          }
      private:
          uint8_t name_length = 12;
    };

To compile code to web assembly ``(.wasm)`` use command:

.. code-block:: console

    $ eosio-cpp name_validator.cpp -o name_validator.wasm

It will return something like:

.. code-block:: bash

    Warning, empty ricardian clause file
    Warning, empty ricardian clause file
    Warning, action <validatename> does not have a ricardian contract

Deploy contract to account
==========================

To start, you need to unlock your wallet:

.. code-block:: console

    $ remcli wallet unlock

Than, enter your wallet password and create account ``validator``:

.. code-block:: console

    $ remcli create account rem validator YOUR_PUBLIC_KEY -p rem@active

.. note::
    Instead, you can use existing keys tied to other account permissions.
    Let's use a key tied to the ``active`` permission of the ``bob`` account for a new account:

    .. code-block:: console

        $ remcli create account rem validator bob@active -p rem@active

Now you can deploy the compiled contract on our account by command:

.. code-block:: console

    $ remcli set contract validator ABSOLUTE_CONTRACT_DIR_PATH/name_validator -p validator@active

It will return something like:

.. code-block:: bash

    Publishing contract...
    executed transaction: fb747edf07b55c6fde304dc065c6a1e93e08066c6f5f110b2a1e8047c9bdc1a5  2592 bytes  738 us
    #           rem <= rem::setcode                 {"account":"validator","vmtype":0,"vmversion":0,"code":"0061736d010000000164126000006000017f60027f7f...
    #           rem <= rem::setabi                  {"account":"validator","abi":"0e656f73696f3a3a6162692f312e3100010c76616c69646174656e616d650001087573...
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

Test contract
=============

| Naming conventions we already define above.

The interface for call actions from the contract is as follows:

.. code-block:: bash

    Push a transaction with a single action
    Usage: remcli push action [OPTIONS] account action data

    Positionals:
      account TEXT                The account providing the contract to execute (required)
      action TEXT                 A JSON string or filename defining the action to execute on the contract (required)
      data TEXT                   The arguments to the contract (required)

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
      -p,--permission TEXT ...    An account and permission level to authorize, as in 'account@permission'
      --max-cpu-usage-ms UINT     set an upper limit in milliseconds of cpu usage budget, for the execution of the transaction (defaults to 0 which means no limit)
      --max-net-usage UINT        set an upper limit on the net usage budget, in bytes, for the transaction (defaults to 0 which means no limit)
      --delay-sec UINT            set the delay_sec seconds, defaults to 0s

| Let's check the valid name ``testaccount1`` by command ``remcli push action ACCOUNT ACTION DATA``:

.. code-block:: console

    $ remcli push action validator validatename '["testaccount1"]' -p rem


| If the name is correct, the action should pass without errors.
| It will return something like:

.. code-block:: bash

    executed transaction: 1bbffc6ddde98dc09a9da044fb6e54636171ae66082fc2b84ff9953da76bacee  112 bytes  264 us
    #     validator <= validator::validatename      {"username":"testaccount1"}
    warning: transaction executed locally, but may not be confirmed by the network yet         ]

| Now, let's test the wrong account name - an account name which is less than 12 characters.
| This should return an error: ``account name must be 12 characters``

.. code-block:: console

    $ remcli push action validator validatename '["test"]' -p rem

Yes, it is, the contract returned an error to us:

.. code-block:: bash

    Error Details:
    assertion failure with message: account name must be 12 characters
    pending console output:

Let's test an existing account:

.. code-block:: console

    $ remcli push action validator validatename '["rem"]' -p rem

It will return something like:

.. code-block:: bash

    Error Details:
    assertion failure with message: account already exists
    pending console output:

Check the last case when the name contains invalid characters, for example ``tes#account``:

.. code-block:: console

    $ remcli push action validator validatename '["tes#account"]' -p rem

This should return an error message:

.. code-block:: bash

    Error Details:
    assertion failure with message: character is not in allowed character set for names
    pending console output:
