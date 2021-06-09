.. _blockdata:

Block data
========================

Block data in Mitum currency node
------------------------------------

* In the Mitum currency node, block data is stored in two spaces: the database and the file system.
* The `database` stores the informations which are used for consensus, such as

.. code-block::

    blockdata_map
    info
    manifest: block header
    operation: operation fact
    operation
    proposal
    seal
    state: state data by each block
    voteproof

* The `file system` stores all block data, such as

.. code-block::

    manifest
    operations of block
    states of block
    proposal
    suffrage information
    voteproofs(and init and accept ballots)

* Block data stored in the database is required to run the Mtum currency node and participate in the network normally. 
* Block data in the file system is not used at runtime, but is used to provide block data to syncing nodes.
* An intact node must support block data for other nodes that want to synchronize block data.

BlockDataMap
---------------

* By default, block data is stored on the local file system.
* BlockDataMap contains the information about where the actual block data is located.

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

* In this BlockDataMap example, the data of suffrage_info is located at file:///000/000/000/000/000/000/010/10-suffrage_info-24d6.jsonld.gz

BlockDataMap for block data stored in external storage
---------------------------------------------------------

* Mitum currency supports storing block data in external storage rather than the node's local file system.
* After going through some process to store block data externally, blockdataMap becomes as follows.

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

* As you can see the url is replaced with the external storage server.

How to update BlockDataMap for external Storage
---------------------------------------------------

* For example, suppose that block data with a blockheight of 10 are moved to an external storage.
* Here we will do this using the node's `deploy key`.
* This `deploy key` of the node is a key that can be used instead of the private key of the node.
* See :ref:`deploy key` for how to create a `deploy key`.
* The process of moving blockdata and updating blockdatamap is as follows.
    * Get the new deploy key of mitum currency node.
    * Download the current BlockDataMap by using the `storage download map` command.
    * Upload all the block data files of height, 10 to external storage(example : AWS S3)
    * Update the url field value of the downloaded BlockDataMap with the new url of external storage.
    * Update the node's BlockdataMap by running the `storage set-blockdatamaps` command.
    * Check the newly updated BlockDataMap with `storage download map` command
* After updating BlockDataMap successfully, Mitum currency node will remove all the files of height, 10 automatically after 30 minute.

.. code-block::

    $ DEPLOY_KEY=d-974702df-89a7-4fd1-a742-2d66c1ead6cd
    $ NODE=quic://127.0.0.1:54330
    $ ./mc storage download map 10 --tls-insecure --node=$NODE > mapData
    $ cat mapData | jq
    {
        "_hint": "0191:0.0.1",
        "hash": "BjrgEX1ziSfSQ1MqAATBLtbXMd7R86snFzCjxVvSCmFH",
        "height": 10,
        "block": "HYDBJkMmJoYFcLL4AHvWYreQBzZLgsv1x7vUFvLPfqte",
        "created_at": "2021-06-09T03:14:15.605Z",
        "items": {
            "states": {
                "type": "states",
                "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
                "url": "file:///000/000/000/000/000/000/010/10-states-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz"
            },
            "manifest": {
                "type": "manifest",
                "checksum": "4007a072f19c9b87e1e370b639a3eea2c2d9438e7be4f577c3f2da6804fc076c",
                "url": "file:///000/000/000/000/000/000/010/10-manifest-4007a072f19c9b87e1e370b639a3eea2c2d9438e7be4f577c3f2da6804fc076c.jsonld.gz"
            },
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025",
                "url": "file:///000/000/000/000/000/000/010/10-operations_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz"
            },
            "operations": {
                "type": "operations",
                "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
                "url": "file:///000/000/000/000/000/000/010/10-operations-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz"
            },
            "proposal": {
                "type": "proposal",
                "checksum": "5c6dc1cd86c0feee423c06a6170548451bd767b7c9dbea67688108899b3981da",
                "url": "file:///000/000/000/000/000/000/010/10-proposal-5c6dc1cd86c0feee423c06a6170548451bd767b7c9dbea67688108899b3981da.jsonld.gz"
            },
            "states_tree": {
                "type": "states_tree",
                "checksum": "d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025",
                "url": "file:///000/000/000/000/000/000/010/10-states_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz"
            },
            "accept_voteproof": {
                "type": "accept_voteproof",
                "checksum": "732b4306d2afcee956ed39490068fc9e4e78f24ecc994bda83f74504cba429ae",
                "url": "file:///000/000/000/000/000/000/010/10-accept_voteproof-732b4306d2afcee956ed39490068fc9e4e78f24ecc994bda83f74504cba429ae.jsonld.gz"
            },
            "suffrage_info": {
                "type": "suffrage_info",
                "checksum": "5a069edd5867509cd2f4db7ece22d3d5b2ef53ee734d92b9c53e3c71a2c2bce4",
                "url": "file:///000/000/000/000/000/000/010/10-suffrage_info-5a069edd5867509cd2f4db7ece22d3d5b2ef53ee734d92b9c53e3c71a2c2bce4.jsonld.gz"
            },
            "init_voteproof": {
                "type": "init_voteproof",
                "checksum": "d96b90f913f1107453f09f5cabc87a2d7eea7c9170fdd3ac49e0445138c4a5b4",
                "url": "file:///000/000/000/000/000/000/010/10-init_voteproof-d96b90f913f1107453f09f5cabc87a2d7eea7c9170fdd3ac49e0445138c4a5b4.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }
    $ aws s3 cp ./blockdata/000/000/000/000/000/000/010 s3://destbucket/blockdata/000/000/000/000/000/000/010 --recursive
    # update mapData blockdata url from "file:///000/000/000/000/000/000/010/" to https://aws/"
    $ ./mc storage set-blockdatamaps $DEPLOY_KEY mapData $NODE --tls-insecure
    $ ./mc storage download map 10 --tls-insecure --node=$NODE
    {
        "_hint": "0191:0.0.1",
        "hash": "BjrgEX1ziSfSQ1MqAATBLtbXMd7R86snFzCjxVvSCmFH",
        "height": 10,
        "block": "HYDBJkMmJoYFcLL4AHvWYreQBzZLgsv1x7vUFvLPfqte",
        "created_at": "2021-06-09T03:14:15.605Z",
        "items": {
            "states": {
                "type": "states",
                "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
                "url": "https://aws/10-states-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz"
            },
            "manifest": {
                "type": "manifest",
                "checksum": "4007a072f19c9b87e1e370b639a3eea2c2d9438e7be4f577c3f2da6804fc076c",
                "url": "https://aws/10-manifest-4007a072f19c9b87e1e370b639a3eea2c2d9438e7be4f577c3f2da6804fc076c.jsonld.gz"
            },
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025",
                "url": "https://aws/10-operations_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz"
            },
            "operations": {
                "type": "operations",
                "checksum": "0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124",
                "url": "https://aws/10-operations-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz"
            },
            "proposal": {
                "type": "proposal",
                "checksum": "5c6dc1cd86c0feee423c06a6170548451bd767b7c9dbea67688108899b3981da",
                "url": "https://aws/10-proposal-5c6dc1cd86c0feee423c06a6170548451bd767b7c9dbea67688108899b3981da.jsonld.gz"
            },
            "states_tree": {
                "type": "states_tree",
                "checksum": "d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025",
                "url": "https://aws/10-states_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz"
            },
            "accept_voteproof": {
                "type": "accept_voteproof",
                "checksum": "732b4306d2afcee956ed39490068fc9e4e78f24ecc994bda83f74504cba429ae",
                "url": "https://aws/10-accept_voteproof-732b4306d2afcee956ed39490068fc9e4e78f24ecc994bda83f74504cba429ae.jsonld.gz"
            },
            "suffrage_info": {
                "type": "suffrage_info",
                "checksum": "5a069edd5867509cd2f4db7ece22d3d5b2ef53ee734d92b9c53e3c71a2c2bce4",
                "url": "https://aws/10-suffrage_info-5a069edd5867509cd2f4db7ece22d3d5b2ef53ee734d92b9c53e3c71a2c2bce4.jsonld.gz"
            },
            "init_voteproof": {
                "type": "init_voteproof",
                "checksum": "d96b90f913f1107453f09f5cabc87a2d7eea7c9170fdd3ac49e0445138c4a5b4",
                "url": "https://aws/10-init_voteproof-d96b90f913f1107453f09f5cabc87a2d7eea7c9170fdd3ac49e0445138c4a5b4.jsonld.gz"
            }
        },
        "writer": "0192:0.0.1"
    }
.. 