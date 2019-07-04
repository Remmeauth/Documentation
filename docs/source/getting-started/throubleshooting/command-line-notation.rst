Command line notation
=====================

Throughout the documentation, we’ll show some commands used in the terminal. Lines that you should enter in a terminal all start with ``$``.
You don’t need to type in the ``$`` character, it indicates the start of each command. Lines that don’t start with ``$`` typically show
the output of the previous command.

The typical command line interface looks like this. There two separated commands, so you should enter it one by one.

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio_1.7.0-1-ubuntu-18.04_amd64.deb
   $ sudo apt install ./eosio_1.7.0-1-ubuntu-18.04_amd64.deb

If you see ``&& \`` symbols at the end of the first command, it means to copy all lines and paste as one command.

.. code-block:: console

   $ wget https://github.com/EOSIO/eos/releases/download/v1.7.0/eosio_1.7.0-1-ubuntu-18.04_amd64.deb && \
         sudo apt install ./eosio_1.7.0-1-ubuntu-18.04_amd64.deb
