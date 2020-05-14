################################
Development Wallet Configuration
################################

``Remvault`` are repositories of public-private key pairs. Private keys are needed to sign operations performed on the blockchain.
``Remvault`` are accessed using ``remcli``.

Step 1: Create a Default Wallet
===============================
To create a wallet use command ``remcli wallet create``.
If using ``remcli`` in production, it's wise to instead use ``--to-file`` so your wallet password is not in your bash history.
For development purposes you can use ``--to-console``.

.. code-block:: console

    $ remcli wallet create --to-console

``remcli`` should return you a password:

.. code-block:: console

    Creating wallet: default
    Save password to use in the future to unlock this wallet.
    Without password imported keys will not be retrievable.
    "PW5JKxKgwfjVeDL7Reqg9RcHn**********Qkg9Taev5S1EKAduff"

.. note::
    Created ``Default`` wallet will be saved to ``~/eosio-wallet/default.wallet``.

Step 2: Open and Unlock Wallet
==============================

Wallets are closed by default when starting a ``remvault`` instance. To begin, run the following:

.. code-block:: console

    $ remcli wallet open

Now, that your wallet is open, you’ll need to unlock it by using password that we generate below.
To unlock your wallet, enter following command:

.. code-block:: console

    $ remcli wallet unlock

Than, enter the password.

.. note::
    You can use flag ``--password`` and unlock wallet by command:

    .. code-block:: console

        $ remcli wallet unlock --password PW5JKxKgwfjVeDL7Reqg9RcHn**********Qkg9Taev5S1EKAduff

The console prints out that your default wallet is unlocked: ``Unlocked: default``

Step 3: Generate a private key
==============================
The following command will generate a private key.

.. code-block:: console

    $ remcli wallet create_key

Step 6: Import the Development Key
==================================

.. code-block:: console

    $ remcli wallet import

You'll be prompted for a private key, enter the ``rem`` development key provided below

.. code-block:: console

    5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

It will return something like:

.. code-block:: console

    imported private key for: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

