.. _blockdata:

BlockData
========================

Data in Mitum 
-----------------

* In Mitum, block is saved in 2 different space: database and blockdata.
* `database` stores the information which are used for consensus, such as

.. code-block::

    manifest: block header
    state: data by each block
    operation fact
    etc

* `blockdata` stores all the data of block, such as

.. code-block::

    manifest
    operations of block
    states of block
    proposal
    suffrage information
    voteproofs(and init and accept ballots)

* For running mitum and participating network normally, database will be needed; blockdata is not used at running time.
* The normal intact node should support the data of blockdata for the other node, syncing.

BlockDataMap
---------------

* Basically blockdata is stored in local filesystem.
* BlockDataMap contains the information where the actual data are located.

.. code-block::

    {
        "_hint": "0191:0.0.1",
        "hash": "J4dV77TH8SXxhhVNoRby1PaWK9iT1eKFLjEcjAL619qF",
        "height": 10,
        "block": "HkKtQdL1Ko2fzgj579MyCY87ffmYGyB8hTpsSpDUvME3",
        "created_at": "2021-05-31T09:33:30.708Z",
        "items": {
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "24d639e2b83ef5a0cb807a527f94b4074b737640aa02f747dd5525087acbf1d0",
            "url": "file:///000/000/000/000/000/000/010/10-suffrage_info-24d6.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
            "url": "file:///000/000/000/000/000/000/010/10-operations-0fed.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }

* In this BlockDataMap, the data of suffrage_info is located at file:///000/000/000/000/000/000/010/10-suffrage_info-24d6.jsonld.gz and this file is manged by blockdata

Non-Local BlockDataMap
------------------------

* Basically the files of blockdata is saved in local filesystem of node.
* Mitum supports non-local BlockDataMap like,

.. code-block::

    {
        "_hint": "0191:0.0.1",
        "hash": "J4dV77TH8SXxhhVNoRby1PaWK9iT1eKFLjEcjAL619qF",
        "height": 10,
        "block": "HkKtQdL1Ko2fzgj579MyCY87ffmYGyB8hTpsSpDUvME3",
        "created_at": "2021-05-31T09:33:30.708Z",
        "items": {
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "24d639e2b83ef5a0cb807a527f94b4074b737640aa02f747dd5525087acbf1d0",
            "url": "https://aws/10-suffrage_info-24d6.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
            "url": "https://aws/10-operations-0fed.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }

How to update BlockDataMap for Non-Local Storage
---------------------------------------------------

* The blockdata files of height, 10 will be copied to aws
    * Get the new deploy key. See here for a detailed description of the deploy key command.
    * Download the existing BlockDataMap file by the storage download map command.
    * Upload all the blockdata files of height, 10 to aws
    * Rewrite the url field value of the downloaded BlockDataMap file with the new url of aws
    * Execute the new command, storage set-blockdatamaps
    * Check the newly updated BlockDataMap file with storage download map command
* After updating BlockDataMap successfully, mitum node will remove all the files of height, 10 automatically after 30 minute

* Existing BlockDataMap of height, 10:

.. code-block::

    {
        "_hint": "0191:0.0.1",
        "hash": "J4dV77TH8SXxhhVNoRby1PaWK9iT1eKFLjEcjAL619qF",
        "height": 10,
        "block": "HkKtQdL1Ko2fzgj579MyCY87ffmYGyB8hTpsSpDUvME3",
        "created_at": "2021-05-31T09:33:30.708Z",
        "items": {
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "24d639e2b83ef5a0cb807a527f94b4074b737640aa02f747dd5525087acbf1d0",
            "url": "file:///000/000/000/000/000/000/010/10-suffrage_info-24d6.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
            "url": "file:///000/000/000/000/000/000/010/10-operations-0fed.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }

* Rewritten BlockDataMap of height, 10 with the new aws url:

.. code-block::

    {
        "_hint": "0191:0.0.1",
        "hash": "J4dV77TH8SXxhhVNoRby1PaWK9iT1eKFLjEcjAL619qF",
        "height": 10,
        "block": "HkKtQdL1Ko2fzgj579MyCY87ffmYGyB8hTpsSpDUvME3",
        "created_at": "2021-05-31T09:33:30.708Z",
        "items": {
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "24d639e2b83ef5a0cb807a527f94b4074b737640aa02f747dd5525087acbf1d0",
            "url": "https://aws/10-suffrage_info-24d6.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
            "url": "https://aws/10-operations-0fed.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }