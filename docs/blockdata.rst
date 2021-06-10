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
        "_hint": "base-blockdatamap-v0.0.1",
        "hash": "DvYK11jZ8KWafAGPssypdNMRwwXwJJTKeyzTAx4JNnwc",
        "height": 10,
        "block": "AnjD39fpP6cJKVhnSfJxPfQ8sxrVwCrKhm1zWjb38dUS",
        "created_at": "2021-06-10T06:37:42.251Z",
        "items": {
            "accept_voteproof": {
            "type": "accept_voteproof",
            "checksum": "03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753",
            "url": "file:///000/000/000/000/000/000/010/10-accept_voteproof-03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753.jsonld.gz"
            },
            "init_voteproof": {
            "type": "init_voteproof",
            "checksum": "70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0",
            "url": "file:///000/000/000/000/000/000/010/10-init_voteproof-70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0.jsonld.gz"
            },
            "states": {
            "type": "states",
            "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
            "url": "file:///000/000/000/000/000/000/010/10-states-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "proposal": {
            "type": "proposal",
            "checksum": "ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465",
            "url": "file:///000/000/000/000/000/000/010/10-proposal-ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465.jsonld.gz"
            },
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e",
            "url": "file:///000/000/000/000/000/000/010/10-suffrage_info-f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e.jsonld.gz"
            },
            "manifest": {
            "type": "manifest",
            "checksum": "1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880",
            "url": "file:///000/000/000/000/000/000/010/10-manifest-1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
            "url": "file:///000/000/000/000/000/000/010/10-operations-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "states_tree": {
            "type": "states_tree",
            "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
            "url": "file:///000/000/000/000/000/000/010/10-states_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
            "operations_tree": {
            "type": "operations_tree",
            "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
            "url": "file:///000/000/000/000/000/000/010/10-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            }
        },
        "writer": "blockdata-writer-v0.0.1"
    }
    $ aws s3 cp ./blockdata/000/000/000/000/000/000/010 s3://destbucket/blockdata/000/000/000/000/000/000/010 --recursive
    # update mapData blockdata url from "file:///000/000/000/000/000/000/010/" to https://aws/"
    $ ./mc storage set-blockdatamaps $DEPLOY_KEY mapData $NODE --tls-insecure
    $ ./mc storage download map 10 --tls-insecure --node=$NODE
    {
        "_hint": "base-blockdatamap-v0.0.1",
        "hash": "DvYK11jZ8KWafAGPssypdNMRwwXwJJTKeyzTAx4JNnwc",
        "height": 10,
        "block": "AnjD39fpP6cJKVhnSfJxPfQ8sxrVwCrKhm1zWjb38dUS",
        "created_at": "2021-06-10T06:37:42.251Z",
        "items": {
            "accept_voteproof": {
            "type": "accept_voteproof",
            "checksum": "03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753",
            "url": "https://aws/10-accept_voteproof-03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753.jsonld.gz"
            },
            "init_voteproof": {
            "type": "init_voteproof",
            "checksum": "70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0",
            "url": "https://aws/10-init_voteproof-70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0.jsonld.gz"
            },
            "states": {
            "type": "states",
            "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
            "url": "https://aws/10-states-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "proposal": {
            "type": "proposal",
            "checksum": "ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465",
            "url": "https://aws/10-proposal-ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465.jsonld.gz"
            },
            "suffrage_info": {
            "type": "suffrage_info",
            "checksum": "f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e",
            "url": "https://aws/10-suffrage_info-f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e.jsonld.gz"
            },
            "manifest": {
            "type": "manifest",
            "checksum": "1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880",
            "url": "https://aws/10-manifest-1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880.jsonld.gz"
            },
            "operations": {
            "type": "operations",
            "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
            "url": "https://aws/10-operations-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "states_tree": {
            "type": "states_tree",
            "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
            "url": "https://aws/10-states_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
            "operations_tree": {
            "type": "operations_tree",
            "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
            "url": "https://aws/10-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            }
        },
        "writer": "blockdata-writer-v0.0.1"
    }
.. 