Keypair
===============

* Private key and public key are created through keypair generation.
* The generated keypair is used to create an account, register a keypair of a node, and create a signature of operation and seal.

.. _create keypair:

Create Keypair 
--------------------

* New keypair can be created as follows.

.. code-block:: sh

      $ ./mc key new
      hint: mpr
      privatekey: L2kcF9mkai2BahAjRj1cghjtMnyEFvadXNVSMzLNSxCbMZyMJyR1mpr
      publickey: 22C9QQ2UUYaUccGvGZPrFZb2PM347sT56xHB5tyNNkTNgmpu

* You can also use the seed to create a new keypair.

.. code-block:: sh

      $ ./mc key new --seed abcdefghijklmnopqrstuvwxyzABCDEFGHIJ
      hint: mpr
      privatekey: KySup78QSWRKU7Y6e2rsPzELfJPq7XuhwfunEmQLPmKaDi6o5Laumpr
      publickey: qQF4jdw4N2wLf86DC6evZrD57VwzuH8sY4a6wAEf42hqmpu

Multi Sig Account
------------------------

* Account is a data structure that has currency and balance in Mitum currency.
* Account has a unique value called address and can be identified through this.
* Register a public key for user's Account authentication.
* Mitum currency accounts can register multiple public keys because multi signatures are possible.

.. csv-table::
   :widths: 30, 150

   "address", "HjyXhhuHAZBGaEw2S5cKZhDwqVc1StbkJMtdgGm3F1dnmca"
   "threshold", "100"
   "keys", "{key: rd89Gx..., weight: 50}, {key: skRdC6..., weight: 50}"
   "balance", "{currency: MCC, amount: 10000}, {currency: MCC2, amount: 20000}"

* Set the threshold value in Account. 1 < threshold <= 100.
* The sum of the weights of the keys should be greater than or equal to the threshold.

.. csv-table:: "case with only one key and threshold 100"
    :widths: 30, 300

    "threshold", 100
    "keys", "{key: rd89Gx..., weight: 100}"
    
.. csv-table:: "case with only one key and threshold 50"
    :widths: 30, 300

    "threshold", 50
    "keys", "{key: rd89Gx..., weight: 60}"

.. csv-table:: "case with multiple keys and threshold 100"
    :widths: 30, 300

    "threshold", 100
    "keys", "{key: rd89Gx..., weight: 40}, {key: skRdC6..., weight: 30}, {key: mymMwq..., weight: 30}"

.. csv-table:: "case with multiple keys and threshold 50"
    :widths: 30, 300

    "threshold", 50
    "keys", "{key: rd89Gx..., weight: 20}, {key: skRdC6..., weight: 20}, {key: mymMwq..., weight: 10}"

* Even in the same *publickey* combination, *address* will have different values if *weight* or *threshold* are different.

.. _check address:

Check Address
---------------

* How to check the address in the public key is as follows.

.. code-block:: sh

      $ ./mc key address <threshold> <publickey>,<weight>

.. code-block:: sh
     
      $ ACC_PUB=22C9QQ2UUYaUccGvGZPrFZb2PM347sT56xHB5tyNNkTNgmpu
      $ THRESHOLD=100
      $ WEIGHT=100
      $ ./mc key address $THRESHOLD $ACC_PUB,$WEIGHT
      D15QgLXgpKFQDLT3hkTdLsqHQAj2tqj7Dj68wRgtwEscmca