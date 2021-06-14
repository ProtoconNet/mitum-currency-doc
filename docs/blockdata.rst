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
        "_hint": "base-blockdatamap-v0.0.1",
        "hash": "2ojLCZwG5J7xmfoxiBbhvJsc6dDTxDFDsw1nfPneT2xr",
        "height": 2,
        "block": "BcXqCKG5MbQcfuFpPtjvHcNBGeK6Pz3aG2cMcp4MUy9C",
        "created_at": "2021-06-14T03:20:24.887Z",
        "items": {
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "file:///000/000/000/000/000/000/002/2-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
        },
        "writer": "blockdata-writer-v0.0.1"
    }



* In this BlockDataMap example, the data of operation_tree is located at file:///000/000/000/000/000/000/002/2-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz

BlockDataMap for block data stored in external storage
---------------------------------------------------------

* Mitum currency supports storing block data in external storage rather than the node's local file system.
* After going through some process to store block data externally, blockdataMap becomes as follows.


.. code-block::

    {
        "_hint": "base-blockdatamap-v0.0.1",
        "hash": "2ojLCZwG5J7xmfoxiBbhvJsc6dDTxDFDsw1nfPneT2xr",
        "height": 2,
        "block": "BcXqCKG5MbQcfuFpPtjvHcNBGeK6Pz3aG2cMcp4MUy9C",
        "created_at": "2021-06-14T03:20:24.887Z",
        "items": {
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "fhttps://aws/2-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
        },
        "writer": "blockdata-writer-v0.0.1"
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
        "hash": "2ojLCZwG5J7xmfoxiBbhvJsc6dDTxDFDsw1nfPneT2xr",
        "height": 2,
        "block": "BcXqCKG5MbQcfuFpPtjvHcNBGeK6Pz3aG2cMcp4MUy9C",
        "created_at": "2021-06-14T03:20:24.887Z",
        "items": {
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "file:///000/000/000/000/000/000/002/2-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
            "manifest": {
                "type": "manifest",
                "checksum": "6e53950e3ab87008b2bcb9841461588456c3e1069458eb8b150f1bfb97d22d42",
                "url": "file:///000/000/000/000/000/000/002/2-manifest-6e53950e3ab87008b2bcb9841461588456c3e1069458eb8b150f1bfb97d22d42.jsonld.gz"
            },
            "suffrage_info": {
                "type": "suffrage_info",
                "checksum": "e7584f9b5324566d4c5319db33ece980000f9c29eaf4d17befcc239743788f02",
                "url": "file:///000/000/000/000/000/000/002/2-suffrage_info-e7584f9b5324566d4c5319db33ece980000f9c29eaf4d17befcc239743788f02.jsonld.gz"
            },
            "states": {
                "type": "states",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "file:///000/000/000/000/000/000/002/2-states-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "operations": {
                "type": "operations",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "file:///000/000/000/000/000/000/002/2-operations-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "proposal": {
                "type": "proposal",
                "checksum": "dbbce4aaa6aece06596ecd45068008d35a41f592339d8898501b55f5843dbefe",
                "url": "file:///000/000/000/000/000/000/002/2-proposal-dbbce4aaa6aece06596ecd45068008d35a41f592339d8898501b55f5843dbefe.jsonld.gz"
            },
            "init_voteproof": {
                "type": "init_voteproof",
                "checksum": "705af3bd660070813354b572288204d787a949fc5411f3e2bc28e86f07bc1e64",
                "url": "file:///000/000/000/000/000/000/002/2-init_voteproof-705af3bd660070813354b572288204d787a949fc5411f3e2bc28e86f07bc1e64.jsonld.gz"
            },
            "accept_voteproof": {
                "type": "accept_voteproof",
                "checksum": "0d4296d44f96a3de216a90f99d77bf77a00ecd5102d7bbba612b13a57bdf2f34",
                "url": "file:///000/000/000/000/000/000/002/2-accept_voteproof-0d4296d44f96a3de216a90f99d77bf77a00ecd5102d7bbba612b13a57bdf2f34.jsonld.gz"
            },
            "states_tree": {
                "type": "states_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "file:///000/000/000/000/000/000/002/2-states_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            }
        },
        "writer": "blockdata-writer-v0.0.1"
    }
    
    $ aws s3 cp ./blockdata/000/000/000/000/000/000/002 s3://destbucket/blockdata/000/000/000/000/000/000/002 --recursive
    # update mapData blockdata url from "file:///000/000/000/000/000/000/002/" to https://aws/"
    $ ./mc storage set-blockdatamaps $DEPLOY_KEY mapData $NODE --tls-insecure
    $ ./mc storage download map 2 --tls-insecure --node=$NODE
    {
        "_hint": "base-blockdatamap-v0.0.1",
        "hash": "2ojLCZwG5J7xmfoxiBbhvJsc6dDTxDFDsw1nfPneT2xr",
        "height": 2,
        "block": "BcXqCKG5MbQcfuFpPtjvHcNBGeK6Pz3aG2cMcp4MUy9C",
        "created_at": "2021-06-14T03:20:24.887Z",
        "items": {
            "operations_tree": {
                "type": "operations_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "fhttps://aws/2-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            },
            "manifest": {
                "type": "manifest",
                "checksum": "6e53950e3ab87008b2bcb9841461588456c3e1069458eb8b150f1bfb97d22d42",
                "url": "fhttps://aws/2-manifest-6e53950e3ab87008b2bcb9841461588456c3e1069458eb8b150f1bfb97d22d42.jsonld.gz"
            },
            "suffrage_info": {
                "type": "suffrage_info",
                "checksum": "e7584f9b5324566d4c5319db33ece980000f9c29eaf4d17befcc239743788f02",
                "url": "fhttps://aws/2-suffrage_info-e7584f9b5324566d4c5319db33ece980000f9c29eaf4d17befcc239743788f02.jsonld.gz"
            },
            "states": {
                "type": "states",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "fhttps://aws/2-states-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "operations": {
                "type": "operations",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "fhttps://aws/2-operations-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
            },
            "proposal": {
                "type": "proposal",
                "checksum": "dbbce4aaa6aece06596ecd45068008d35a41f592339d8898501b55f5843dbefe",
                "url": "fhttps://aws/2-proposal-dbbce4aaa6aece06596ecd45068008d35a41f592339d8898501b55f5843dbefe.jsonld.gz"
            },
            "init_voteproof": {
                "type": "init_voteproof",
                "checksum": "705af3bd660070813354b572288204d787a949fc5411f3e2bc28e86f07bc1e64",
                "url": "fhttps://aws/2-init_voteproof-705af3bd660070813354b572288204d787a949fc5411f3e2bc28e86f07bc1e64.jsonld.gz"
            },
            "accept_voteproof": {
                "type": "accept_voteproof",
                "checksum": "0d4296d44f96a3de216a90f99d77bf77a00ecd5102d7bbba612b13a57bdf2f34",
                "url": "fhttps://aws/2-accept_voteproof-0d4296d44f96a3de216a90f99d77bf77a00ecd5102d7bbba612b13a57bdf2f34.jsonld.gz"
            },
            "states_tree": {
                "type": "states_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "fhttps://aws/2-states_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
            }
        },
        "writer": "blockdata-writer-v0.0.1"
    }
    
.. 