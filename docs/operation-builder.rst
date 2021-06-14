Using Operation Builder
=============================

* Digest API has Operation Builder to help write operation messages.
* Operation Builder makes it possible to generate operation messages through api without using sdk.
  
Get operation fact template
-------------------------------------------------

* By requesting an Operation fact template, you can receive a template for each operation type.
* You can create a fact message by changing the field value of the template.


| method : GET
| path : /builder/operation/fact/template/{fact}
| response examples

.. code-block::

    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
        "_embedded": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "3Zdg5ZVdNFRbwX5WU7Nada3Wnx5VEgkHrDLVLkE8FMs1",
            "token": "cmFpc2VkIGJ5",
            "sender": "mother:mca-v0.0.1",
            "items": [
                {
                    "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                    "keys": {
                        "_hint": "mitum-currency-keys-v0.0.1",
                        "hash": "2TQ8Xn5tdowqkJt8kHWcNj2QKhuNRnnCwiXxFbRbwBWY",
                        "keys": [
                            {
                                _hint": "mitum-currency-key-v0.0.1",
                                "weight": 100,
                                "key": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H:btc-pub-v0.0.1"
                            }
                        ],
                        "threshold": 100
                    },
                    "amounts": [
                        {
                            "_hint": "mitum-currency-amount-v0.0.1",
                            "amount": "-333",
                            "currency": "xXx"
                        }
                    ]
                }
            ]
        },
        "_links": {
            "self": {
                "href": "/builder/operation/fact/template/create-accounts"
            }
        },
        "_extra": {
            "default": {
                "items.keys.keys.key": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H:btc-pub-v0.0.1"
                "items.big": "-333",
                "currency": "xXx",
                "token": "cmFpc2VkIGJ5",
                "sender": "mother:mca-v0.0.1",
            }
        }
    }

* The _embedded object among the contents of the template responded represents the fact.
* Edit the contents of the fact json object and use it in ``Build operation message``.
* create-accounts fact example.

.. code-block::


    {
        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
        "hash": "3Zdg5ZVdNFRbwX5WU7Nada3Wnx5VEgkHrDLVLkE8FMs1",
        "token": "cmFpc2VkIGJ5",
        "sender": "mother:mca-v0.0.1",
        "items": [
            {
                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                "keys": {
                    "_hint": "mitum-currency-keys-v0.0.1",
                    "hash": "2TQ8Xn5tdowqkJt8kHWcNj2QKhuNRnnCwiXxFbRbwBWY",
                    "keys": [
                        {
                            _hint": "mitum-currency-key-v0.0.1",
                            "weight": 100,
                            "key": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H:btc-pub-v0.0.1"
                        }
                    ],
                    "threshold": 100
                },
                "amounts": [
                    {
                        "_hint": "mitum-currency-amount-v0.0.1",
                        "amount": "-333",
                        "currency": "xXx"
                    }
                ]
            }
        ]
    } 

* The hash value is automatically completed by the builder. You don't have to edit it.
* token is a base64 encoded value.
* Please check :ref:`create keypair` for the details of key registration of accounts related to keys.
* Use the _hint item as it is.

Build operation message
-------------------------------

* The created fact message is sent to the request body in json format and the completed fact message is received.
* In the case of the example, you will receive a fact message with the keys hash, token, and fact hash changed.

| method : POST
| path : /builder/operation/fact
| request body

.. code-block::json

    {
        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
        "hash": "3Zdg5ZVdNFRbwX5WU7Nada3Wnx5VEgkHrDLVLkE8FMs1",
        "token": "cmFpc2VkIGJ5",
        "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
        "items": [
            {
            "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
            "keys": {
                "_hint": "mitum-currency-keys-v0.0.1",
                "hash": "2TQ8Xn5tdowqkJt8kHWcNj2QKhuNRnnCwiXxFbRbwBWY",
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



| Response Example

.. code-block::

    HTTP/1.1 200 OK
    Content-Type: application/hal+json
    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-create-accounts-operation-v0.0.1",
        "_embedded": {
            "hash": "92FXbSdm46iuA7kQuC6ENfi5pd64G1Uiu49A3VmaA8Tu",
            "fact": {
                "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                "hash": "9ttqrz1bkFNCySVnrhYrxewcVB6mkZWWvBpSPS2fShip",
                "token": "MjAyMS0wNi0xNSAwODo0OTozOS45NDggKzAwMDAgVVRD",
                "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                                "amount": "333",
                                "currency": "MCC"
                            }
                        ]
                    }
                ]
            },
            "fact_signs": [
                {
                    "_hint": "base-fact-sign-v0.0.1",
                    "signer": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H:btc-pub-v0.0.1",
                    "signature": "22UZo26eN",
                    "signed_at": "2020-10-08T07:53:26Z"
                }
            ],
            "memo": "",
            "_hint": "mitum-currency-create-accounts-operation-v0.0.1"
        },
        "_links": {
            "self": {
                "href": "/builder/operation/fact"
            }
        },
        "_extra": {
            "default": {
                "fact_signs.signer": "oRHdEPPrgbfNxUp6TWsC35DmWu1zbLCW9rp41Z8npF8H:btc-pub-v0.0.1",
                "fact_signs.signature": "22UZo26eN"
            },
            "signature_base": "hCi8MFOChFusqKx6v0zrsJ8u3tppYUOewadYjwTvDUFtaXR1bQ=="
        }
    }

* Check the fact.hash value of the response data.
* Uses the fact.hash value as data to complete the value of the fact_sign object.
* The signer is the publickey of the keypair used to create the signature.
* The signature is generated by the signer.
* signed_at is the datetime at which the signature was generated.

Sign operation message
----------------------------

* A signature is created using the hash of the received fact and the fact_sign is added.
* When the generated fact message is sent to the request body in json format, the completed Operation message with the operation hash added is received.

| method : POST
| path : /builder/operation/sign
| request body example

.. code-block:: 

    {
        "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
        "fact": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
            "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
            "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                            "amount": "333",
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
                "signature": "AN1rKvtVhunuSdS8g3KWQ1PFBEP9bzz4sU4Vb3B4JrYyVUF79XwNUrG6AzoVfq6mHsK8W4S5hu7LKjDARfAQeDWwit1GnKXcN",
                "signed_at": "2021-06-16T01:56:14.124268Z"
            }
        ],
        "memo": "",
    }



response example

.. code-block::

    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-create-accounts-operation-v0.0.1",
        "_embedded": {
            "fact": {
                "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
                "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                                "amount": "333",
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
                    "signature": "AN1rKvtVhunuSdS8g3KWQ1PFBEP9bzz4sU4Vb3B4JrYyVUF79XwNUrG6AzoVfq6mHsK8W4S5hu7LKjDARfAQeDWwit1GnKXcN",
                    "signed_at": "2021-06-16T01:56:14.124268Z"
                }
            ],
            "memo": "",
            "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
            "hash": "9pNsg6gkQJoVsB7iqY3udeLVti2Yxgbe4mFkGqzds2AT"
        },
        "_links": {
            "self": {
                "href": "/builder/operation/sign"
            }
        }
    }    

Broadcast message to network
--------------------------------------

* By requesting an Operation or Seal message as the request body, you can broadcast it to the network.
* In this case, the signer of the seal becomes the digest node.
* If the request body is operation, a new seal is created and the digest node signs.
* If the request body is a seal, the seal is signed by the digest node.

| method : POST
| path : /builder/send
| request body example

.. code-block::

    {
        "fact": {
            "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
            "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
            "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
            "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                            "amount": "333",
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
                "signature": "AN1rKvtVhunuSdS8g3KWQ1PFBEP9bzz4sU4Vb3B4JrYyVUF79XwNUrG6AzoVfq6mHsK8W4S5hu7LKjDARfAQeDWwit1GnKXcN",
                "signed_at": "2021-06-16T01:56:14.124268Z"
            }
        ],
        "memo": "",
        "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
        "hash": "9pNsg6gkQJoVsB7iqY3udeLVti2Yxgbe4mFkGqzds2AT"
    }


response example

.. code-block::

    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "seal-v0.0.1",
        "_embedded": {
            "_hint": "seal-v0.0.1",
            "hash": "4UvusVw9RYdqxHQz2EzDb6gW6CgoZGPayD1yZBcdSSHW",
            "body_hash": "9AFx2gAqeMveV6ojwUi6HKx19GfbZZggPTGhTS3dDih5",
            "signer": "uGnKHNfh8EtNVXsL4Qu1a655oQuzibK8Tc41TZUHzHqk:btc-pub-v0.0.1",
            "signature": "381yXZAzT6LcYUXfTG9Fifc6neDfXDqpjzuGzfqr1LXPMvvtseJKzGSRwdL6jvkHBaVRdGPD4YfrHnp2rbpZEEWRNAePiJBt",
            "signed_at": "2021-06-16T03:06:33.649190888Z",
            "operations": [
                {
                    "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                    "hash": "9pNsg6gkQJoVsB7iqY3udeLVti2Yxgbe4mFkGqzds2AT",
                    "fact": {
                        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                        "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
                        "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                        "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                                        "amount": "333",
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
                            "signature": "AN1rKvtVhunuSdS8g3KWQ1PFBEP9bzz4sU4Vb3B4JrYyVUF79XwNUrG6AzoVfq6mHsK8W4S5hu7LKjDARfAQeDWwit1GnKXcN",
                            "signed_at": "2021-06-16T01:56:14.124268Z"
                        }
                    ],
                    "memo": ""
                }
            ]
        },
        "_links": {
            "self": {
                "href": ""
            },
            "operation:0": {
                "href": "/block/operation/CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE"
            }
        }
    }


.. _Operation Reason:

Confirming the success of the operation
-------------------------------------------

* Whether the operation is successfully processed can be checked by querying the operation with the fact hash value in the api.
* GET https://api_url/block/operation/{operation_fact_hash}
* If the ``_embedded.in_state`` value is ``true`` in the response message, the operation is saved in the block.
* If the value of ``_embedded.in_state`` is ``false``, the operation was not saved in the block.
* If the operation fails, the reason may be as follows.
* In case of insufficient balance of sender when sending money, incorrect signature, creation-account, amount less than new-account-min-balance, etc.
* You can check the reason for failure in ``_embedded.reason.msg`` in the response message.


.. code-block:: json


    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-operation-value-v0.0.1",
        "_embedded": {
            "_hint": "mitum-currency-operation-value-v0.0.1",
            "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
            "operation": {
                "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                "hash": "9pNsg6gkQJoVsB7iqY3udeLVti2Yxgbe4mFkGqzds2AT",
                "fact": {
                    "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                    "hash": "CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE",
                    "token": "MjAyMS0wMy0yNCAwMjozNzozNC4xNzQgKzAwMDAgVVRD",
                    "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
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
                                    "amount": "333",
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
                        "signature": "AN1rKvtVhunuSdS8g3KWQ1PFBEP9bzz4sU4Vb3B4JrYyVUF79XwNUrG6AzoVfq6mHsK8W4S5hu7LKjDARfAQeDWwit1GnKXcN",
                        "signed_at": "2021-06-16T01:56:14.124Z"
                    }
                ],
                "memo": ""
            },
            "height": 108674,
            "confirmed_at": "2021-06-16T02:26:55.75Z",
            "reason": {
                "_hint": "base-operation-reason-v0.0.1",
                "msg": "state, \"GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca:account\" does not exist",
                "data": null
            },
            "in_state": false,
            "index": 0
        },
        "_links": {
            "manifest": {
                "href": "/block/108674/manifest"
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
                "href": "/block/operation/CDUkHDJB4aC8552QvVCAPk8ZtohSuow67cPZZxqZG7RE"
            },
            "block": {
                "href": "/block/108674"
            }
        }
    }