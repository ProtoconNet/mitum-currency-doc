Keypair
===============

* Private key and public key are created through keypair generation.
* The generated keypair is used to create an account, register a keypair of a node, and create a signature of operation and seal.

.. _create keypair:

Create Keypair 
--------------------

* New keypair can be created as follows.

.. code-block:: sh

      $ ./bin/mc key new --type=<key type>

* In Mitum, you can use bitcoin, ethereum, and stellar keypairs.
* You can select btc, ether, or stellar for the key type. (default: btc)

.. code-block:: sh

      $ ./bin/mc key new --type btc
            hint: hint{type="btc-privatekey" code="0112" version="0.0.1"}
      privatekey: KyJFEE8GpjBUDJbtEz5NW2QndUs4o994zJn1mstYR6Uc5U37BWv6-0112:0.0.1
       publickey: zwaGS678yT5HieAao45sbM3f6x4VAK19NZENQSNdMAGa-0113:0.0.1

Multi Sig Account
------------------------

* Account is a data structure that has currency and balance in Mitum currency.
* Account has a unique value called address and can be identified through this.
* Register a public key for user's Account authentication.
* Mitum currency accounts can register multiple public keys because multi signatures are possible.

.. csv-table::
   :widths: 30, 150

   "address", "5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1"
   "threshold", "100"
   "keys", "{key: rd89Gx..., weight: 50}, {key: skRdC6..., weight: 50}"
   "balance", "{currency: MCC, amount: 10000}, {currency: MCC2, amount: 20000}"

* Set the threshold value in Account. 1 < threshold <= 100.
* The sum of the weights of the keys should be 100.
* 
.. csv-table:: "case with only one key"
    :widths: 30, 300

    "keys", "{key: rd89Gx..., weight: 100}                                                           "

.. csv-table:: "case with multiple keys"
    :widths: 30, 300

    "keys", "{key: rd89Gx..., weight: 40}, {key: skRdC6..., weight: 30}, {key: mymMwq..., weight: 30}"

* Even in the same *publickey* combination, *address* will have different values if *weight* or *threshold* are different.

.. _check address:

Check Address
---------------

* How to check the address in the public key is as follows.

.. code-block:: sh

      $ ./bin/mc key address <threshold> <publickey>,<weight>

.. code-block:: sh
     
      $ ACC_PUB=042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1
      $ THRESHOLD=100
      $ WEIGHT=100
      $ ./bin/mc key address $THRESHOLD $ACC_PUB,$WEIGHT
        HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1