.. _seal send:

Seal Send
==================================

* Operations created in Mitum currency are transmitted in units of seals.
* Signature is required to transmit the seal. Refer to the Seal section in :ref:`Send message to node` for the part related to the keypair used for signature creation.

.. code-block:: sh

    $ ./mc seal send <sender privatekey> --network-id=<network id> --seal=<data file path> --node=<node quic url>

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ NODE="quic://127.0.0.1:54330"
    $ AC0_PRV=L1jPsE8Sjo5QerUHJUZNRqdH1ctxTWzc1ue8Zp2mtpieNwtCKsNZ-0112:0.0.1
    $ ./mc seal send --network-id="$NETWORK_ID" $AC0_PRV --seal=data.json --node=$NODE jq -R '. as $line | try fromjson catch $line'
    {
        "_hint": "seal-v0.0.1",
        "hash": "6nLRWj5hGQ7va9gxpAJCBxNDKvgFnms9jaa913uWgsx1",
        "body_hash": "32ZEf8V9fV41JHVWbbqQdYWtrw5T255XN8fSXhBAhGFD",
        "signer": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1",
        "signature": "381yXZ4LFY5HnK211gpG3W22V52vMLqix4SysXEeMnqcXUk5eEYGM1JfFaX5UE86EF6qog5jUScPqZo6UkiaAFocUhwtSsjx",
        "signed_at": "2021-06-10T09:17:51.236729Z",
        "operations": [
            {
                "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                "hash": "7YvcA6WAcKEag1Z4Jv1bQ2wYxAZix5sNB6u8MUXDM44D",
                "fact": {
                    "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                    "hash": "3equMRJAVHk8WdVanffzEWkHfwnBDqF2cFwmmcv8MzDW",
                    "token": "MjAyMS0wNi0xMFQwOToxNzo1MS4yMDgwOTVa",
                    "sender": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn:mca-v0.0.1",
                    "items": [
                        {
                            "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                            "keys": {
                                "_hint": "mitum-currency-keys-v0.0.1",
                                "hash": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv",
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
                                    "amount": "100000",
                                    "currency": "MCC"
                                }
                            ]
                        }
                    ]
                },
                "fact_signs": [
                    {
                        "_hint": "base-fact-sign-v0.0.1",
                        "signer": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1",
                        "signature": "AN1rKvtPEX4MRu6kWRYDJ6WtsSnwxwJsYXiVi2Qujx8sF6SJzsZZKj7anCd9cmUZ175FSYLkkWkpDRj3fVgZFDxLFSnos3szz",
                        "signed_at": "2021-06-10T09:17:51.211816Z"
                    }
                ],
                "memo": ""
            }
        ]
    }
    2021-06-10T09:17:51.240066Z INF trying to send seal module=command-send-seal
    2021-06-10T09:17:51.345243Z INF sent seal module=command-send-seal

* When sending to a local node for testing, an error may occur related to tls authentication.
* In this case, set --tls-insecure=true and send.

.. code-block:: sh

    $ ./mc seal send --network-id="$NETWORK_ID" $AC0_PRV --tls-insecure=true --seal=data.json --node=$NODE

* Whether the operation is successfully processed can be checked through the api.
* For more information, please refer to :ref:`Operation Reason`.