.. _create-account:

Create Account
==================================

create-account Operation
--------------------------   

* ``create-account`` is an operation which creates new account.
* Register publickey as the key of a new account. The sum of the weights of the keys should be ``100``.

.. code-block:: sh

    $ ./mc seal create-account --network-id=NETWORK-ID-FLAG <privatekey> <sender> <currency> <big>

* We will proceed with the process of creating two accounts, ac0 and ac1 as an example.
* When registering one key per account, two public keys are required.
* For how to create a keypair, please refer to :ref:`create keypair` .
* The operation that creates account ac0 is as follows.

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ GENESIS_PRV=L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok:btc-priv-v0.0.1
    $ GENESIS_ADDR=GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1
    $ AC0_PUB=cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1
    $ ./mc seal create-account --network-id="$NETWORK_ID" $GENESIS_PRV $GENESIS_ADDR XXX 50 --key=$AC0_PUB,100 | jq
    {
        "_hint": "seal-v0.0.1",
        "hash": "Xr7HS7rnbfxTrNbr6qRJ64on6KFuMzvJf5Z6BGqVZsX",
        "body_hash": "EJ93htxhUh2edJhBujMCHhpvGGHQoBic8KQ7VzggxKw1",
        "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
        "signature": "381yXZUffVp3gmKD2WJA6756SeDy16d3PF6Ym15HBL89rs1YhT1cW4zVnWD17mhBdhfhutu3848GPd9zTMDqUFmkE8rUWmCs",
        "signed_at": "2021-06-10T14:06:17.60152Z",
        "operations": [
            {
                "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                "hash": "8ezjZDuC44U2ZFPDkebMyLEYNQBPUUnRjHyfSTeQs9gk",
                "fact": {
                    "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                    "hash": "F1o51xXWnnQYUVV6JA44beJeKKxuJi3Tv8DzvREodHhA",
                    "token": "MjAyMS0wNi0xMFQxNDowNjoxNy41OTczMDNa",
                    "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
                    "items": [
                        {
                            "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                            "keys": {
                                "_hint": "mitum-currency-keys-v0.0.1",
                                "hash": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn",
                                "keys": [
                                    {
                                        "_hint": "mitum-currency-key-v0.0.1",
                                        "weight": 100,
                                        "key": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1"
                                    }
                                ],
                                "threshold": 100
                            },
                            "amounts": [
                                {
                                    "_hint": "mitum-currency-amount-v0.0.1",
                                    "amount": "500",
                                    "currency": "MCC"
                                }
                            ]
                        }
                    ]
                },
                "fact_signs": [
                    {
                        "_hint": "base-fact-sign-v0.0.1",
                        "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
                        "signature": "381yXYyRo91cqu5gFp5GtHWCiYmsssbFxx95MaL8gH4koBCZ5AfnRqYEpWMxcxgKmeEWsRPVJ8zWytAMLiA9zQes9qGnbcj8",
                        "signed_at": "2021-06-10T14:06:17.601089Z"
                    }
                ],
                "memo": ""
            }
        ]
    }

* The above json messages are put in the seal and sent to the node.

.. note::
    * In Mitum currency, two or more operations signed by one account are not processed in one block.
    * For example, two operations that send ``5`` amount from ``ac0'' to ``ac1`` and ``ac2`` cannot be processed at the same time.
    * In this case, only the operation that arrived first is processed and the rest are ignored.

.. code-block:: sh

    $ NETWORK_ID=mitum
    $ NODE=quic://127.0.0.1:54330
    $ GENESIS_PRV=L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok:btc-priv-v0.0.1
    $ GENESIS_ADDR=GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1
    $ CURRENCY_ID=MCC
    $ AC0_PUB=cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1
    $ AC1_PUB=sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1
    $ ./mc seal create-account --network-id="$NETWORK_ID" \
      $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 50 \
      --key=$AC0_PUB,100 |
    ./mc seal create-account --network-id="$NETWORK_ID" \
      $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 50 \
      --key=$AC1_PUB,100 --seal=- | \
    ./mc seal send --network-id="$NETWORK_ID" \
        $GENESIS_PRV --seal=- --node=$NODE --tls-insecure | jq -R '. as $line | try fromjson catch $line'

    {
      "_hint": "seal-v0.0.1",
      "hash": "Fup759XEwxedA16ZNK2Qc3Xpe6c4GcAKJwwyaCnVKFEh",
      "body_hash": "6RP8EXGdY3u6UzqtoNNcsAmpFRRAYr3cUqNUQ42tKSAD",
      "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
      "signature": "AN1rKvt5J5QPg22X9oLksveo9413sjhtL9mJ7wxf7kuo5oxPwYtPtVsDZF9tZdB3H99xPCJW6UarReuxYCJKtdiPxxea41da1",
      "signed_at": "2021-06-10T15:01:12.817304Z",
      "operations": [
        {
          "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
          "hash": "4nmNLangQcL5Ax35NCSfNKiYvoW35knKH4p7t5BVhSD6",
          "fact": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "Dg4Uh7iJQTJE14FhFkR38ctKKedX9CRaURvfCWG4DtvX",
            "token": "MjAyMS0wNi0xMFQxNTowMToxMi44MTI3OVo=",
            "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
            "items": [
              {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                  "_hint": "mitum-currency-keys-v0.0.1",
                  "hash": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn",
                  "keys": [
                    {
                      "_hint": "mitum-currency-key-v0.0.1",
                      "weight": 100,
                      "key": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amounts": [
                  {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "500",
                    "currency": "MCC"
                  }
                ]
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "base-fact-sign-v0.0.1",
              "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
              "signature": "AN1rKvtT5JfDeuFyCy3kiWwGkaAy9AYeEd2RtxdSr1dpuurSZCc1uAapx9qaRDK5WxdU69RwaSTHXyLUo4rCtEA4UaUfHS91B",
              "signed_at": "2021-06-10T15:01:12.816836Z"
            }
          ],
          "memo": ""
        }
      ]
    }
    {
      "_hint": "seal-v0.0.1",
      "hash": "HV1tT3D639TiYe6bmamXtesvNjAN8tJ7AmgmeB6STrwz",
      "body_hash": "Gg5KQzzNPAt5PiLrcE5kjMbd4jB7Vk4ooBmN81yWDqYv",
      "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
      "signature": "381yXZ1szjaYdxsznCpSvg19yS1tKUw1yPmgXBX6Ehf5ZcKNaMCRkJ8PaNS34rUwLSZ88EPh8vFq1FfRncHiTfo1v9adHCSH",
      "signed_at": "2021-06-10T15:01:13.080144Z",
      "operations": [
        {
          "memo": "",
          "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
          "hash": "AhqQMGZHDCeJDp74aQJ8rEXMC6GgQtpxP3rXnjjP41ui",
          "fact": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "3fDBD1i6V5VpGxB1di6JGgMPhyWZeWRML8FX4LnYXqJE",
            "token": "MjAyMS0wNi0xMFQxNTowMToxMy4wNDA0OTZa",
            "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
            "items": [
              {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                  "_hint": "mitum-currency-keys-v0.0.1",
                  "hash": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn",
                  "keys": [
                    {
                      "_hint": "mitum-currency-key-v0.0.1",
                      "weight": 100,
                      "key": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amounts": [
                  {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "50",
                    "currency": "MCC"
                  }
                ]
              },
              {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                  "_hint": "mitum-currency-keys-v0.0.1",
                  "hash": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL",
                  "keys": [
                    {
                      "_hint": "mitum-currency-key-v0.0.1",
                      "weight": 100,
                      "key": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amounts": [
                  {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "50",
                    "currency": "MCC"
                  }
                ]
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "base-fact-sign-v0.0.1",
              "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
              "signature": "AN1rKvthtCymTu7gv2fSrMhGwqVuK3o24FrDe6GGLzRU8N5SWF62nPs3iKcEjuzwHya6P9JmrNLRF95ri8QTE4NBc66TxhCHm",
              "signed_at": "2021-06-10T15:01:13.053303Z"
            }
          ]
        }
      ]
    }
    "2021-06-10T15:01:13.083634Z INF trying to send seal module=command-send-seal"
    "2021-06-10T15:01:13.171266Z INF sent seal module=command-send-seal"

* Whether the operation block is saved can be checked through the ``fact.hash`` of operation inquiry in the digest API.

.. code-block:: sh

    $ FACT_HASH=3fDBD1i6V5VpGxB1di6JGgMPhyWZeWRML8FX4LnYXqJE
    $ DIGEST_API="https://127.0.0.1:54320"
    $ curl --insecure -v $DIGEST_API/block/operation/$FACT_HASH | jq
    {
      "_hint": "mitum-currency-hal-v0.0.1",
      "hint": "mitum-currency-operation-value-v0.0.1",
      "_embedded": {
        "_hint": "mitum-currency-operation-value-v0.0.1",
        "hash": "3fDBD1i6V5VpGxB1di6JGgMPhyWZeWRML8FX4LnYXqJE",
        "operation": {
          "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
          "hash": "AhqQMGZHDCeJDp74aQJ8rEXMC6GgQtpxP3rXnjjP41ui",
          "fact": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "3fDBD1i6V5VpGxB1di6JGgMPhyWZeWRML8FX4LnYXqJE",
            "token": "MjAyMS0wNi0xMFQxNTowMToxMy4wNDA0OTZa",
            "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
            "items": [
              {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                  "_hint": "mitum-currency-keys-v0.0.1",
                  "hash": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn",
                  "keys": [
                    {
                      "_hint": "mitum-currency-key-v0.0.1",
                      "weight": 100,
                      "key": "cnMJqt1Q7LXKqFAWprm6FBC7fRbWQeZhrymTavN11PKJ:btc-pub-v0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amounts": [
                  {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "50",
                    "currency": "MCC"
                  }
                ]
              },
              {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                  "_hint": "mitum-currency-keys-v0.0.1",
                  "hash": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL",
                  "keys": [
                    {
                      "_hint": "mitum-currency-key-v0.0.1",
                      "weight": 100,
                      "key": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1"
                    }
                  ],
                  "threshold": 100
                },
                "amounts": [
                  {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "50",
                    "currency": "MCC"
                  }
                ]
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "base-fact-sign-v0.0.1",
              "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
              "signature": "AN1rKvthtCymTu7gv2fSrMhGwqVuK3o24FrDe6GGLzRU8N5SWF62nPs3iKcEjuzwHya6P9JmrNLRF95ri8QTE4NBc66TxhCHm",
              "signed_at": "2021-06-10T15:01:13.053Z"
            }
          ],
          "memo": ""
        },
        "height": 13,
        "confirmed_at": "2021-06-10T15:01:13.354Z",
        "reason": null,
        "in_state": true,
        "index": 0
      },
      "_links": {
        "block": {
          "href": "/block/13"
        },
        "manifest": {
          "href": "/block/13/manifest"
        },
        "new_account:EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn": {
          "href": "/account/EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn:mca-v0.0.1",
          "address": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn:mca-v0.0.1",
          "key": "EbVibuKTyPqRVRcCpMRQdP7wBkr33GW2brSQvZQNJDSn"
        },
        "new_account:EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL": {
          "href": "/account/EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1",
          "key": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL",
          "address": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1"
        },
        "operation:{hash}": {
          "templated": true,
          "href": "/block/operation/{hash:(?i)[0-9a-z][0-9a-z]+}"
        },
        "block:{height}": {
          "templated": true,
          "href": "/block/{height:[0-9]+}"
        },
        "self": {
          "href": "/block/operation/3fDBD1i6V5VpGxB1di6JGgMPhyWZeWRML8FX4LnYXqJE"
        }
      }
    }

* Whether the operation is successfully processed can be checked through the api.
* For more information, please refer to :ref:`Operation Reason`.