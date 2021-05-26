.. _Send the seal:

Seal and Operation
============================


Operation
---------------

* In the Mitum blockchain network, an operation is a unit of command that changes data.
* Mitum currency has operations of create-account, transfer, key-updater, currency-register, and currency-policy-updater.
* Each operation requires a signature made with a private key according to its contents.
* The fact in the operation contains the contents to be executed, and the hash value summarizing the body of the fact is also included.

Seal
------------

* Seal is a collection of operations transmitted to the network. In other words, the Operation is contained in the seal and transmitted.
* To transmit the seal, a signature made with a private key is required.
* To create Signature, you must use the private key created in Mitum's keypair package.
* The private key used for the signature has nothing to do with the blockchain account. In other words, it doesn't have to be the private key used by the account.
* Seal can contain up to 100 operations.

Send
---------

* After creating an operation, the client creates and attaches a signature.
* Create as many operations as necessary within the maximum number that can be included in the seal and put them in the seal.
* Create and put a signature on the seal.
* Send seal to Mitum node.
  
Stored in block
----------------

* The operation transmitted to the Blockchain network changes the state of the account if it is normal and is finally saved in the block.
* Whether the operation is saved in the block can be checked through digest API.
* Please refer to the :ref:`Operation Reason` here for how to check through the API.z