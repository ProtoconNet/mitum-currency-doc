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

        $ ./mc node info quic://127.0.0.1:54330 --tls-insecure | jq
        {
            "_hint": "mitum-currency-node-info-v0.0.1",
            "node": {
                "_hint": "base-node-v0.0.1",
                "address": "mc-node:sa-v0.0.1",
                "publickey": "27P4S2FdDALmg4QzShCDTDne1pe8y1H2bE2uQCVpnqWpu:btc-pub-v0.0.1",
                "url": "quic://127.0.0.1:54330"
            },
            "network_id": "bWl0dW0=",
            "state": "CONSENSUS",
            "last_block": {
                "_hint": "block-manifest-v0.0.1",
                "hash": "5Z2SFA6DqYg8KdRPAD4uXAM7wpPE6vjyQ5iWqu4sc1yP",
                "height": 421,
                "round": 0,
                "proposal": "3H5wmRqvnburtEMqvkLh11vetbbdsdvHAkJRM6L6nu3Z",
                "previous_block": "J3if3xYD1wUQxUnm52UpddHT4Dipsd35bYGQxurMGnXm",
                "block_operations": null,
                "block_states": null,
                "confirmed_at": "2021-06-10T07:04:31.378699784Z",
                "created_at": "2021-06-10T07:04:31.390856784Z"
            },
            "version": "v0.0.0",
            "url": "quic://127.0.0.1:54330",
            "policy": {
                "network_connection_timeout": 3000000000,
                "max_operations_in_seal": 10,
                "max_operations_in_proposal": 100,
                "interval_broadcasting_init_ballot": 1000000000,
                "wait_broadcasting_accept_ballot": 1000000000,
                "threshold": 100,
                "interval_broadcasting_accept_ballot": 1000000000,
                "timeout_waiting_proposal": 5000000000,
                "timespan_valid_ballot": 60000000000,
                "interval_broadcasting_proposal": 1000000000,
                "suffrage": "{\"type\":\"\",\"cache_size\":10,\"number_of_acting\":1}"
            },
            "suffrage": [
                {
                    "_hint": "base-node-v0.0.1",
                    "address": "mc-node:sa-v0.0.1",
                    "publickey": "27P4S2FdDALmg4QzShCDTDne1pe8y1H2bE2uQCVpnqWpu:btc-pub-v0.0.1",
                    "url": "quic://127.0.0.1:54330"
                }
            ]
        }
