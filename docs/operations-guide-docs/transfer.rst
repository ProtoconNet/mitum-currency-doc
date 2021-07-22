.. _transfer token:

Transfer token
==================

transfers Operation
----------------------

* Transfers Operation is used to transfer coins between created accounts.

.. code-block:: sh

    $ ./mc seal transfer --network-id=NETWORK-ID-FLAG <privatekey> <sender> <receiver> <currency> <big>

* This is an example of transferring the currency ``MCC`` amount, ``3`` from ``ac0`` to ``ac1``

.. code-block:: sh

    $ AC0_PRV=KzUYFHNzxvUnZfm1ePJJ4gnLcLtMv1Tvod7Fib2sRuFmGwzm1GVb:btc-priv-v0.0.1
    $ AC0_ADDR=381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1
    $ AC1_ADDR=EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1
    $ CURRENCY_ID=MCC
    $ NETWORK_ID="mitum"
    $ ./mc seal transfer --network-id="$NETWORK_ID" $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq

    {
        "_hint": "seal-v0.0.1",
        "hash": "EJDzHbusvvcknN9NWaK1wjuvSTav2TVfnDmtRnqVjEVn",
        "body_hash": "FWLTyQePguo6CFxH8SgEHesoLL8ab3FofEw9nXHDDLMp",
        "signer": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1",
        "signature": "381yXZMbRqwMgfWwJNk4rWNuaJenJMHZU3HBufz7Uo4Yj3zo944oeJeGoKjUDyCJXuL4pZLt49gqW2FHV3YuB5zBR24h96ZH",
        "signed_at": "2021-06-14T03:42:11.969679Z",
        "operations": [
            {
                "_hint": "mitum-currency-transfers-operation-v0.0.1",
                "hash": "F3WZYRgcwwYENiVXx6J6zKPqkiDjSZcuF2vUUPiyR3n9",
                "fact": {
                    "_hint": "mitum-currency-transfers-operation-fact-v0.0.1",
                    "hash": "7xzioXfnkKU1qrFvgeWK1KrhR71RMHMSBZdpWRVK3MUD",
                    "token": "MjAyMS0wNi0xNFQwMzo0MjoxMS45NjUyNjNa",
                    "sender": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
                    "items": [
                        {
                            "_hint": "mitum-currency-transfers-item-single-amount-v0.0.1",
                            "receiver": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1",
                            "amounts": [
                                {
                                    "_hint": "mitum-currency-amount-v0.0.1",
                                    "amount": "10",
                                    "currency": "MCC"
                                }
                            ]
                        }
                    ]
                },
                "fact_signs": [
                    {
                        "_hint": "base-fact-sign-v0.0.1",
                        "signer": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1",
                        "signature": "AN1rKvtRQeMWcFQ9oPLqgakgW33fed4mCcxxfQwi3icWLyn19AKJ3XpYehA8njvAi7qzgGSVpv23JXBDcXbwiZvQkHBj6T8jw",
                        "signed_at": "2021-06-14T03:42:11.96891Z"
                    }
                ],
                "memo": ""
            }
        ]
    }


    $ ./mc seal transfer --network-id="$NETWORK_ID" $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq \
      ./mc seal send --network-id="$NETWORK_ID" $AC0_PRV --seal=-

* Whether the operation is successfully processed can be checked through the api.
* For more information, please refer to :ref:`Operation Reason`.