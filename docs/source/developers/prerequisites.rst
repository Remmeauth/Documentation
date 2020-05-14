#############
Prerequisites
#############

Blockchain Environments
=======================

+---------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
|                            Service                            | Description                                                                                   |
+---------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| `Remprotocol <https://github.com/Remmeauth/remprotocol>`_     | Remprotocol Blockchain source files.                                                          |
|                                                               | `Install Remprotocol <preparation-step.html>`_ to get started.                                |
+---------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| `Rem.contracts <https://github.com/Remmeauth/rem.contracts>`_ |  | Remprotocol system contracts. Can be used to obtain system tables                          |
|                                                               |  | by importing contacts.                                                                     |
+---------------------------------------------------------------+-----------------------------------------------------------------------------------------------+
| `Eosio CDT <https://github.com/EOSIO/eosio.cdt>`_             | EOSIO Contract Development Toolkit.                                                           |
+---------------------------------------------------------------+-----------------------------------------------------------------------------------------------+

Development Tools
=================

| You can use any text editor that, preferably, supports C++ syntax highlighting.
| Some popular editors and IDEs:

* `CLion <https://www.jetbrains.com/clion/>`_

* `Eclipse <http://www.eclipse.org/downloads/packages/release/oxygen/1a/eclipse-ide-cc-developers>`_

* `Visual Studio Code <https://code.visualstudio.com/>`_

* `Atom Editor <https://atom.io/>`_

Also, you can try IDEs specifically developed for EOSIO:

- `EOS Studio <https://www.eosstudio.io/>`_

Remprotocol Mainnet
===================

+---------------------------+----------------------------+----------------------------------------------+
|          Service          | URL                        | Description                                  |
+---------------------------+----------------------------+----------------------------------------------+
| Blockchain URL            | https://remchain.remme.io/ | | Used to make API calls to set/get          |
|                           |                            | | information from/to Remchain.              |
+---------------------------+----------------------------+----------------------------------------------+
| Blockchain P2P            | p2p.remchain.remme.io:2087 | | The address of a node hosted by Remme      |
|                           |                            | | for synchronizing a producer or full node. |
+---------------------------+----------------------------+----------------------------------------------+
| Blockchain Explorer       | https://remme.bloks.io/    | Bloks.io block explorer.                     |
+---------------------------+----------------------------+----------------------------------------------+
| Remme Blockchain Explorer | https://remchain.remme.io/ | Remme block explorer.                        |
+---------------------------+----------------------------+----------------------------------------------+

Remprotocol Testnet
===================

+---------------------------+-----------------------------+----------------------------------------------+
|          Service          | URL                         | Description                                  |
+---------------------------+-----------------------------+----------------------------------------------+
| Blockchain URL            | https://testchain.remme.io/ | | Used to make API calls to set/get          |
|                           |                             | | information from/to Testchain.             |
+---------------------------+-----------------------------+----------------------------------------------+
| Blockchain P2P            | p2p.testchain.remme.io:2087 | | The address of a node hosted by Remme      |
|                           |                             | | for synchronizing a producer or full node. |
+---------------------------+-----------------------------+----------------------------------------------+
| Remme Blockchain Explorer | https://testchain.remme.io/ | Remme block explorer.                        |
+---------------------------+-----------------------------+----------------------------------------------+

.. note::
    | To use the ``Remchain mainnet`` you need to make a swap `ERC20 - > Remprotocol <https://remme.io/blog/remchain-mainnet-live>`_,
      you can swap tokens back any time.
    | To use the ``Remchain testnet`` you need to create account and get tokens from ``FaucetBot``, here are the `instructions <deploy-to-testchain.html>`_.
