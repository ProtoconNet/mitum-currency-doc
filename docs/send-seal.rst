.. _Send the seal:

Seal and Operation
============================


Operation
---------------

* In the Mitum blockchain network, an operation is a unit of command that changes data.
* Mitum currency has operations of create-account, transfer, key-updater, currency-register, and currency-policy-updater.
* Each operation requires a signature made with a private key according to its contents.
* The fact in the operation contains the contents to be executed, and the hash value summarizing the body of the fact is also included.

Fact and token
-----------------

* Every operation contains a fact. The content of the operation is actually contained in the fact. 
* Facts play an important role in Mitum currency. The fact hash is a value representing the processed operation.
* So to check whether the operation is stored in the block, it can be retrieved using the fact hash.
* Therefore, the fact hash must have a unique value in the blockchain.
* In fact, the contents of the facts can be duplicated. For example, the contents that sender A sends 100 to receiver B must always have the same fact.
* Fact hashes created using the same fact content result in duplicate values.
* If there are two or more operations that result in duplicate values ​​of the fact hash Only the first operation is processed and the remaining operations are ignored.
* If so, does that mean that operations with the same fact content cannot be duplicated?
* Don't worry, in fact we use a value called token to make a fact unique.
* The token is a value added to the essential contents of the operation.

.. code-block::

    {
        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
        "hash": "3Zdg5ZVdNFRbwX5WU7Nada3Wnx5VEgkHrDLVLkE8FMs1",
        "token": "cmFpc2VkIGJ5",
        "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
        "items": [
            {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                    "_hint": "mitum-currency-keys-v0.0.1",
                    "keys": [
                        {
                            "_hint": "mitum-currency-key-v0.0.1",
                            "weight": 100,
                            "key": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1"
                        }
                    ],
                    "threshold": 100
                },
                "amounts": [
                    {
                        "_hint": "mitum-currency-amount-v0.0.1",
                        "amount": "333",
                        "currency": "MCC"
                    }
                ]
            }
        ]
    }


* A token is similar to a memo, but has the characteristic of making a fact unique.
* Of course, in the case of using a unique token value for the same fact content.
* Making the fact that is essential to every operation unique expands usability in many ways.
* The biggest advantage is that if you know exactly the contents of the fact along with the token, you can simply check whether the operation is processed or not.
* Anyone can calculate the fact hash if they know the sender, receiver, currencyID, amount, and a specific token value was used.
* Therefore, anyone can inquire whether the corresponding operation has been processed with the fact hash
* A fact hash is like a public proof recorded in a blockchain. If the evidence disclosed in the blockchain is used well, various applications can be made.
* For example, even an outsider who does not have a direct account in the blockchain can check the fact hash, which is the only value indicating whether the operation is processed or not, and make the implementation conditional on this.
* In addition, facts and tokens can be usefully used in models that deal with various data as well as remittance.


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