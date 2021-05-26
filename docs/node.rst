``node`` Command
===================

* ``node`` command initializes node and runs node.
* The subcommands of the ``node`` command are as follows.
  
    * ``init`` : It is executed with the node design file containing the node configuration and initializes the node.
    
        *  See :ref:`node initialization` for a detailed explanation of the ``init`` command.
    
    * ``run`` : It runs with the node design file containing the node configuration and runs the node.

        * See :ref:`make node run` for a detailed explanation of the ``run`` command.

    * ``info`` : It is executed with the url of the remote node and gets the information of the node.

    .. code-block::

        $ mitum-currency node info quic://127.0.0.1:54330
        {
            "_hint": "a015:0.0.1",
            "node": {
                "_hint": "0170:0.0.1",
                "address": "n0-010a:0.0.1",
                "publickey": "skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1",
                "url": "quic://mitum-currency-0:54330"
            },
            "network_id": "bWl0dW0=",
            "state": "CONSENSUS",
            "last_block": {
                "_hint": "0141:0.0.1",
                "hash": "C2JQ8ADT5zDzAx9kao8okhBFXw5xHUhB3FJhV5UginLX",
                "height": 339806,
                "round": 0,
                "proposal": "HU1gMH5xtJ4haSmwg5REvrd6sXDZJeM9SqFTFZQ8NBjo",
                "previous_block": "3YnjGpoXmHGcJquXzZbhvEDB3ubWKQnSmV1bPPbRh9cv",
                "block_operations": null,
                "block_states": null,
                "confirmed_at": "2021-05-25T06:16:13.279580731Z",
                "created_at": "2021-05-25T06:16:13.31476915Z"
            },
            "version": "v0.0.1",
            "url": "quic://mitum-currency-0:54330",
            "policy": {
                "max_operations_in_seal": 100,
                "max_operations_in_proposal": 100,
                "network_connection_timeout": 3000000000,
                "suffrage": "{\"number_of_acting\":1,\"type\":\"\",\"cache_size\":10}",
                "threshold": 67,
                "timeout_waiting_proposal": 5000000000,
                "interval_broadcasting_proposal": 1000000000,
                "wait_broadcasting_accept_ballot": 1000000000,
                "interval_broadcasting_accept_ballot": 1000000000,
                "interval_broadcasting_init_ballot": 1000000000,
                "timespan_valid_ballot": 60000000000
            },
            "suffrage": [
                {
                "_hint": "0170:0.0.1",
                "address": "n0-010a:0.0.1",
                "publickey": "skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1",
                "url": "quic://mitum-currency-0:54330"
                },
                {
                "_hint": "0170:0.0.1",
                "address": "n2-010a:0.0.1",
                "publickey": "wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1",
                "url": "quic://mitum-currency-2:54330?insecure=true"
                },
                {
                "_hint": "0170:0.0.1",
                "address": "n3-010a:0.0.1",
                "publickey": "vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1",
                "url": "quic://mitum-currency-3:54330?insecure=true"
                }
            ]
        }
