#####################
Smart Contract Basics
#####################

A smart contract in ``Remprotocol`` consists of ``actions`` and ``persistent storage`` (tables).
The contract can perform all the basic actions as a regular account that are determined by its logic.

Action
======

Push Action Interface
=====================

``Actions`` determine the basic functionality of your smart contract that affects the state of the network.

.. code-block:: console

    $ remcli push action [OPTIONS] account action data

    Positionals:
      account TEXT                The account providing the contract to execute (required)
      action TEXT                 A JSON string or filename defining the action to execute on the contract (required)
      data TEXT                   The arguments to the contract (required)

Permission System
==================

| With the flexibility of the permissions levels on the ``Remprotocol``, you can restrict access to your ``actions`` in a
  smart contract by including ``require_auth()`` method in your ``actions``.
| ``Restricted Access Action`` Example:

.. code-block:: c++

    [[eosio::action]]
    void adduser( name user, string metadata ) {
        require_auth( get_self() );
        auto it = users.find(user.value);
        check(it == rewards_tbl.end(), "account already exists");

        users.modify(*it, get_self(), [&](auto &u) {
            u.user     = user;
            u.metadata = metadata;
            u.balance  = 0;
        });
    }

| You can find more information about the `Permission System <https://developers.eos.io/welcome/latest/protocol/accounts_and_permissions>`_ here.

Persist Data
============

| Each time a smart contract action is called, a ``wasm code`` is executed that in turn creates an instance that is destroyed
  after the ``wasm code`` is executed. A smart contract does not store the state of instance after their destruction.
| ``Multi-index`` or ``Singleton`` tables are used to persist data between actions.

.. code-block:: c++

    struct [[eosio::table, eosio::contract("CONTRACT_NAME")]] users {
         name      user;
         string    metadata;
         uint64_t  balance;

         uint64_t primary_key() const { return account.value; }
      };

| You can find more information about the `Persist Data <https://developers.eos.io/eosio-home/docs/data-persistence>`_.

Dispatchers
===========

Every smart contract must provide an ``apply`` action handler.
The ``apply`` action handler is a function that listens to all incoming actions and performs the desired behavior.
In order to respond to a particular action, code is required to identify and respond to specific action requests.
``apply`` uses the ``receiver``, ``code``, and ``action`` input parameters as filters to map to the desired functions that implement
particular actions. To simplify the work for contract developers, EOSIO provides the ``EOSIO_DISPATCH`` macro,
which encapsulates the lower level action mapping details of the ``apply`` function, enabling developers to focus on their
application implementation.

.. code-block:: c

    #include <eosio/eosio.hpp>

    using namespace eosio;

    class [[eosio::contract]] accounting_system : public contract {
      public:
          using contract::contract;

          [[eosio::action]]
          void adduser( name user, string metadata ) {
             require_auth( get_self() );
             auto it = users.find(user.value);
             check(it == rewards_tbl.end(), "account already exists");

             users.modify(*it, get_self(), [&](auto &u) {
                u.user     = user;
                u.metadata = metadata;
                u.balance  = 0;
            });
          }
      private:
        struct [[eosio::table]] users {
           name      user;
           string    metadata;
           uint64_t  balance;

           uint64_t primary_key() const { return account.value; }
        };
        typedef eosio::multi_index<"users"_n, users> users_index;
    };
    EOSIO_DISPATCH(accounting_system, (adduser))

| Refer to EOSIO’s `glossary <https://developers.eos.io/welcome/latest/glossary/index/#dispatcher>`_.

