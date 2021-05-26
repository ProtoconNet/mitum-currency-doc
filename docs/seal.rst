``seal`` Command
===================

* ``seal`` command executes various operations contained in the seal.
* The subcommands related to ``seal`` command are as follows.
  
    * ``create-account`` : Create an account.
    
        *  See :ref:`create-account` for a detailed explanation of the ``create-account`` command.
    
    * ``transfer`` : Transfer tokens between accounts.

        * See :ref:`transfer token` for a detailed explanation of the ``transfer`` command.

    * ``key-updater`` : Update the account keys.

        * See :ref:`update key` for a detailed explanation of the ``key-updater`` command.

    * ``currency-register`` : Register a new currency token.

        * See :ref:`register currency` for a detailed explanation of the ``currency-register`` command.

    * ``currency-policy-updater`` : Update the policy related to currency.

        * See :ref:`currency policy update` for a detailed explanation of the ``currency-policy-updater`` command.

* ``seal`` command also creates a signature and sends a seal.


* The subcommands related to signature generation and transmission are as follows.

    * ``send`` : Send a seal.
        
        *  See :ref:`seal send` for a detailed explanation of the ``send`` command.

    * ``sign`` : Create a signature for a seal.
        
        *  Prepare a file in which operation contents to be included in the seal are saved in json format for signature generation.

    .. code-block:: json

        {
            "_hint": "0151:0.0.1",
            "hash": "HReASqf3Y3V5V3LUgzJciMgS4od1Za6pYqiGspyTR48b",
            "body_hash": "2iKPpcoExmxEnS6pFgJEonJvH4irudWT3Bqpxj5P2yw8",
            "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
            "signature": "AN1rKvtgDF8cnCJDzKGXt8Ky7q3anKKBHXqjLwNFRGPHu6VipFNcHkC8LndUPEcdggS7o9itE1CbXeTsEy9pCuSCw4DhHaqjD",
            "signed_at": "2021-05-25T08:54:17.115855Z",
            "operations": [
                {
                    "_hint": "a002:0.0.1",
                    "hash": "KCegFHXZ4bjBHTK8bRAKWgfQf7ZDMNuCLwFB1BBVodA",
                    "fact": {
                        "_hint": "a001:0.0.1",
                        "hash": "HMuPVdmksH3wNHLDYXLcQuUuF1znT1kW5i2wZFafCsg1",
                        "token": "MjAyMS0wNS0yNVQwODo1NDoxNy4xMTQ4MDZa",
                        "sender": "4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1",
                        "items": [
                            {
                                "_hint": "a027:0.0.1",
                                "receiver": "5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1",
                                "amounts": [
                                    {
                                        "_hint": "a022:0.0.1",
                                        "amount": "100",
                                        "currency": "MCC"
                                    }
                                ]
                            }
                        ]
                    },
                    "fact_signs": [
                        {
                            "_hint": "0150:0.0.1",
                            "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
                            "signature": "AN1rKvtRqZ8Y1FhHoW8vXntqiVfcSG619QAZL7GVGd2KpfRSDXG7sFtXYAnS3ZCpaKscLvweKX5RCQxw9TbGUeUExwqe2xsLX",
                            "signed_at": "2021-05-25T08:54:17.115525Z"
                        }
                    ],
                    "memo": ""
                }
            ]
        }

    .. code-block:: sh

        $ SIGNER_PRV=L5GTSKkRs9NPsXwYgACZdodNUJqCAWjz2BccuR4cAgxJumEZWjok-0112:0.0.1
        $ mitum-currency seal sign --seal=data.json  --network-id=mitum $SIGNER_PRV | jq
        {
            "_hint": "0151:0.0.1",
            "hash": "3qhmaLHPSFeFEBTwV4Uow23WRsGRA3B1wCWburFTLPvS",
            "body_hash": "8yQtRY7aQWx5YoSMeA7qfPWPL4bkhiVDZmyXnkmareWF",
            "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
            "signature": "AN1rKvt1aAjgxc8sm3v8Kb3PFVonvpovYEYi9qwcbUULJJBStNqXaXuET96TK6eVtDY9WzEVUAtE88sYyML9mL51uqZ2wJNE5",
            "signed_at": "2021-05-25T09:18:52.388474Z",
            "operations": [
            {
                "_hint": "a006:0.0.1",
                "hash": "EYQ3fdAHgY9FvZknHHhRLqmKp3gFkeJ9A4cXevcg5UCi",
                "fact": {
                "_hint": "a005:0.0.1",
                "hash": "2YRRFJASgRvm6pxWb8FeWswYZvFTVTncZnuis9KdnfDu",
                "token": "MjAyMS0wNS0yNVQwOToxODo1Mi4zODcyMTZa",
                "sender": "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1",
                "items": [
                    {
                    "_hint": "a025:0.0.1",
                    "keys": {
                        "_hint": "a004:0.0.1",
                        "hash": "HT5K9UFrodcVSTjmSzzRfLMykN99jpJU5BkFatdGnrsw",
                        "keys": [
                        {
                            "_hint": "a003:0.0.1",
                            "weight": 100,
                            "key": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT-0113:0.0.1"
                        }
                        ],
                        "threshold": 100
                    },
                    "amounts": [
                        {
                        "_hint": "a022:0.0.1",
                        "amount": "10000",
                        "currency": "MCC"
                        }
                    ]
                    }
                ]
                },
                "fact_signs": [
                {
                    "_hint": "0150:0.0.1",
                    "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG-0113:0.0.1",
                    "signature": "381yXZLqghQx39zrFxMnUyYrXVYfhFrxGV2LYDPix7yGsySTJtTXnFkvgZzyE4zkAooxCv6SDxNbt1qisLAjm2qJAag2unUK",
                    "signed_at": "2021-05-25T09:18:52.388218Z"
                }
                ],
                "memo": ""
            }
            ]
        }

    * ``sign-fact`` : create signature for operation facts.

        * This command is used to add a fact signature to the operation contained in the seal.
        * Therefore, you must pass the seal data containing the operation to this command.
        * The purpose of use is in the case of an operation created by an account with multisig 
        * or when signing of nodes is required such as currency registration.
        * This example seal data contains the operation of transfer from the multi sig account. 
        * It requires two fact signatures, but has only one.

    .. code-block:: json

        {
            "_hint": "0151:0.0.1",
            "hash": "3eyKJMyji8JnzmDXkdutwy4G257ys4vtZBpeD8XcDy2w",
            "body_hash": "3rrMdHkPynqcCaCfevr84oe9bnftbHxm9k1FofdPLa8K",
            "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
            "signature": "381yXZNsXfeMvp8Y1x4iJm4eFkQNd3PsvzkMCbZyHqU62w75hYpgbU4wpraii3eMRyTcBVRGXjjgjxVERzc2Rcd6kEWJ18JV",
            "signed_at": "2021-05-26T03:50:09.501864Z",
            "operations": [
                {
                    "memo": "",
                    "_hint": "a002:0.0.1",
                    "hash": "FsnHR8j4trgMBsFJDTPNUVqGWVQehLz2A2aGnqAmEspp",
                    "fact": {
                        "_hint": "a001:0.0.1",
                        "hash": "6TWmZaUV36DRV6Vy56Ma1mevCEwt7Fefojf2Gxmz8T14",
                        "token": "MjAyMS0wNS0yNlQwMzo1MDowOS41MDA5NzRa",
                        "sender": "BQJNvfhxkomiJ9uBDSHTdtbuhsXmF4ZsrEhRzhMfkCnh-a000:0.0.1",
                        "items": [
                            {
                                "_hint": "a027:0.0.1",
                                "receiver": "CxHHFrekGKFsVKmaTKNfwhxD7KHzZ9sbhBiaREatpRWY-a000:0.0.1",
                                "amounts": [
                                    {
                                        "_hint": "a022:0.0.1",
                                        "amount": "100",
                                        "currency": "MCC"
                                    }
                                ]
                            }
                        ]
                    },
                    "fact_signs": [
                        {
                            "_hint": "0150:0.0.1",
                            "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
                            "signature": "AN1rKvtRJ2eWPuxZeQrkKgooMWnRWRjPp4LBMm3qdpvFwFTDhCnLGUq3SRFafmhqshe9oFVBw5EVoCGz4w6UyctS8oJyFGJZt",
                            "signed_at": "2021-05-26T03:50:09.501603Z"
                        }
                    ]
                }
            ]
        }

    * Use the ``sign-fact`` command to add a fact signature.

    .. code-block:: sh

        $ SIGNER1_PUB_KEY=rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1
        $ SIGNER2_PUB_KEY=sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT-0113:0.0.1
        $ SIGNER2_PRV_KEY=L5AAoEqwnHCp7WfkPcUmtUX61ppZQww345rEDCwB33jVPud4hzKJ-0112:0.0.1
        $ NETWORK_ID=mitum
        $ mitum-currency seal sign-fact $SIGNER2_PRV_KEY --seal data.json --network-id=$NETWORK_ID | jq

        {
            "_hint": "0151:0.0.1",
            "hash": "2g3gNCv58vc5k3fi36wRrUGm8qLLS3rkkU1anvNRCEyG",
            "body_hash": "56ha6EbT1AsvuXT1KdUg5NwjU2kUbb7hwMFRXnjUbaMm",
            "signer": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT-0113:0.0.1",
            "signature": "381yXZ37Zbc6nxhaEAUDusg35hXXDZj3xzudBXn92bkXKQRAi79SQtCNePkNEwojmW3GPhsGer4LsaPPkLa4LHDbeKmsZx2R",
            "signed_at": "2021-05-26T03:50:41.689783Z",
            "operations": [
                {
                    "fact_signs": [
                        {
                            "_hint": "0150:0.0.1",
                            "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
                            "signature": "AN1rKvtRJ2eWPuxZeQrkKgooMWnRWRjPp4LBMm3qdpvFwFTDhCnLGUq3SRFafmhqshe9oFVBw5EVoCGz4w6UyctS8oJyFGJZt",
                            "signed_at": "2021-05-26T03:50:09.501603Z"
                        },
                        {
                            "_hint": "0150:0.0.1",
                            "signer": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT-0113:0.0.1",
                            "signature": "AN1rKvt8SFaUdJjTbgjermuMvMDTatyP5UWVw86qJXbvQLTbZufbx8UKsPF2MTgW3tTJJLviFWoqG9YCBdNkVQfvBTBELHbM6",
                            "signed_at": "2021-05-26T03:50:41.689592Z"
                        }
                    ],
                    "memo": "",
                    "_hint": "a002:0.0.1",
                    "hash": "AbR71584EGcZsZSY6HnZpFBtDgxuQWy1e9PpYh1zPBWh",
                    "fact": {
                        "_hint": "a001:0.0.1",
                        "hash": "6TWmZaUV36DRV6Vy56Ma1mevCEwt7Fefojf2Gxmz8T14",
                        "token": "MjAyMS0wNS0yNlQwMzo1MDowOS41MDA5NzRa",
                        "sender": "BQJNvfhxkomiJ9uBDSHTdtbuhsXmF4ZsrEhRzhMfkCnh-a000:0.0.1",
                        "items": [
                            {
                                "_hint": "a027:0.0.1",
                                "receiver": "CxHHFrekGKFsVKmaTKNfwhxD7KHzZ9sbhBiaREatpRWY-a000:0.0.1",
                                "amounts": [
                                    {
                                        "_hint": "a022:0.0.1",
                                        "amount": "100",
                                        "currency": "MCC"
                                    }
                                ]
                            }
                        ]
                    }
                }
            ]
        }