###########
What's next
###########

Data Persistence
================
| The next step in learning smart contracts is Data Persistence.
  We've already explained this `here <smart-contract-basics.html#persist-data>`_, and recommend that you familiarize yourself with this in more detail.

Refer to EOSIO’s:

- `Data Persistence <https://developers.eos.io/welcome/v2.0/getting-started/smart-contract-development/data-persistence>`_
- `Secondary Indices <https://developers.eos.io/welcome/v2.0/getting-started/smart-contract-development/secondary-indices>`_

Inline Actions
==============
We have already explained what an action is; it’s also important to understand how to construct actions,
and send those actions from within a contract.

.. note::
    Inline actions request other actions that need to be executed as part of the original calling action.
    Inline actions operate with the same scope and authority as the original transaction, and are guaranteed to
    execute with the current transaction. These can effectively be thought of as nested transactions within the calling
    transaction. If any part of the transaction fails, the inline actions will unwind with the rest of the transaction.

    | Refer to EOSIO’s glossary: `Inline Action <https://developers.eos.io/welcome/latest/glossary/index/#inline-action>`_

For the next tutorial, you’ll need an understanding of how inline actions work.
To get acquainted with this in more detail, refer to EOSIO’s:

- `Adding Inline Actions <https://developers.eos.io/welcome/v2.0/getting-started/smart-contract-development/adding-inline-actions>`_
- `Inline Actions to External Contracts <https://developers.eos.io/welcome/v2.0/getting-started/smart-contract-development/inline-action-to-external-contract>`_

