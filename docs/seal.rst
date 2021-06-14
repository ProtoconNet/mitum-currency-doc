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
            "_hint": "seal-v0.0.1",
            "hash": "5W39B2mmtc4KK9THiRdoF6F5UMZPSxjzedPePojVhqyV",
            "body_hash": "5yGtCzJiPRRbZkeLawQev4dvdYgYuKHXe6TP6x2VLSt4",
            "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
            "signature": "381yXZHsyzbc8qTD7BJgmGoM8ncSrUcyDZiSNanARp9h84tvcj6HkGXzpFyck9arJTCQDmPGzT5UFq1coHv7wijusgynSfgr",
            "signed_at": "2021-06-10T06:50:26.903245Z",
            "operations": [
                {
                    "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                    "hash": "9mFHaqd66pv7RjoAbKScUucJLKW7KVSkWqN1WXnzMrxQ",
                    "fact": {
                        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                        "hash": "3CpL1MgD1TPejUmVxPKSgiUu6LCR7FhFrDehSjSogavZ",
                        "token": "MjAyMS0wNi0xMFQwNjo1MDoyNi44NzQyNzVa",
                        "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
                        "items": [
                            {
                                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                                "keys": {
                                    "_hint": "mitum-currency-keys-v0.0.1",
                                    "hash": "Dut3WiprEo1BRcx2xRvh6qbBgxaTLXQDris7SihDTET8",
                                    "keys": [
                                        {
                                            "_hint": "mitum-currency-key-v0.0.1",
                                            "weight": 100,
                                            "key": "27tMvbSpajF1VSnrn3xRQESpPAsmA7KZEfUz9ZuTZEemu:btc-pub-v0.0.1"
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
                            "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
                            "signature": "AN1rKvtfRrgY15owfURsNyfWnYtZ7syuRafWa637tkWB1HyxDCD2tWZUhySTg6mnZWQKpP3i6Dmf96fw9TUWb8rrbsetHJciH",
                            "signed_at": "2021-06-10T06:50:26.877954Z"
                        }
                    ],
                    "memo": ""
                }
            ]
        }

    .. code-block:: sh

        $ SIGNER_PRV=KxmWM4Zj5Ln8bbDwVZEKrYQY8N51Uk3UVq5GNQAeb2KW8JqHmsgm:btc-priv-v0.0.1
        $ ./mc seal sign --seal=data.json  --network-id=mitum $SIGNER_PRV | jq
        {
            "_hint": "seal-v0.0.1",
            "hash": "5dLCySkPrFtc8SnbjzELBK5GR7VQocrK7cXswEnhEa1S",
            "body_hash": "3Ah7J2q4HhFXSgV3c4EQWeZtpi1nFY7be2nmL4X6qDxa",
            "signer": "224ekkhrax6EpekzfLTv9See1hNDZW3LAjWBRuzTMpgnr:btc-pub-v0.0.1",
            "signature": "AN1rKvtFhZfDzyLLXtK3PtZ8P1jSTqZy6gC8WooBjWRhzwLrXjCcVTeo4juzdMg83he2emJ3SVkCNZssiB1pTtAPtx753P5CT",
            "signed_at": "2021-06-10T07:12:41.992205Z",
            "operations": [
                {
                    "_hint": "mitum-currency-create-accounts-operation-v0.0.1",
                    "hash": "9mFHaqd66pv7RjoAbKScUucJLKW7KVSkWqN1WXnzMrxQ",
                    "fact": {
                        "_hint": "mitum-currency-create-accounts-operation-fact-v0.0.1",
                        "hash": "3CpL1MgD1TPejUmVxPKSgiUu6LCR7FhFrDehSjSogavZ",
                        "token": "MjAyMS0wNi0xMFQwNjo1MDoyNi44NzQyNzVa",
                        "sender": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
                        "items": [
                            {
                                "_hint": "mitum-currency-create-accounts-single-amount-v0.0.1",
                                "keys": {
                                    "_hint": "mitum-currency-keys-v0.0.1",
                                    "hash": "Dut3WiprEo1BRcx2xRvh6qbBgxaTLXQDris7SihDTET8",
                                    "keys": [
                                        {
                                            "_hint": "mitum-currency-key-v0.0.1",
                                            "weight": 100,
                                            "key": "27tMvbSpajF1VSnrn3xRQESpPAsmA7KZEfUz9ZuTZEemu:btc-pub-v0.0.1"
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
                            "signer": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1",
                            "signature": "AN1rKvtfRrgY15owfURsNyfWnYtZ7syuRafWa637tkWB1HyxDCD2tWZUhySTg6mnZWQKpP3i6Dmf96fw9TUWb8rrbsetHJciH",
                            "signed_at": "2021-06-10T06:50:26.877954Z"
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
            "_hint": "seal-v0.0.1",
            "hash": "CgFaHkJEP966xRQjzPtXBUwzqgQYWB53RHwjBqyvmKHs",
            "body_hash": "Akjx1kJZKzyYMo2eVbqcUvtEfivDEGsK4yeUUuNwbGmu",
            "signer": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1",
            "signature": "381yXZ8qZBYQXDBaGr1KyAcsMJyB9HZLo1aQQRsxhx854aMYm5n7nh3NXzsJHpEhiYHgWUYnCtbAZaVsQ8pe6nEnLaHCXizY",
            "signed_at": "2021-06-10T09:54:35.868873Z",
            "operations": [
                {
                    "hash": "Eep8SJH7Vkqft3BcvKYd9NY14Zgzmhyp7Uts2GmpaS5N",
                    "fact": {
                        "_hint": "mitum-currency-transfers-operation-fact-v0.0.1",
                        "hash": "Eu1b4gr528Xy4u2sg97DsEo5uj9BuQEMjHzJxdsLgH48",
                        "token": "MjAyMS0wNi0xMFQwOTo1NDozNS44NjQwOTha",
                        "sender": "3TNoGhXH4HaXHb12PE3MhXRRNGLvcVJFfh9fUjrWFp83:mca-v0.0.1",
                        "items": [
                            {
                                "_hint": "mitum-currency-transfers-item-single-amount-v0.0.1",
                                "receiver": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
                                "amounts": [
                                    {
                                    "_hint": "mitum-currency-amount-v0.0.1",
                                    "amount": "100",
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
                            "signature": "AN1rKvtZFkx5e4NexvBSjjJkuzUj45UKau8DL2JZx5d1htnbnkmPmHnNbgwqfvUnz8KHpUR72Z9YxD4JVQhdh4JCzGv9zMDDG",
                            "signed_at": "2021-06-10T09:54:35.868223Z"
                        }
                    ],
                    "memo": "",
                    "_hint": "mitum-currency-transfers-operation-v0.0.1"
                }
            ]
        }

    * Use the ``sign-fact`` command to add a fact signature.

    .. code-block:: sh

        $ SIGNER1_PUB_KEY=2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1
        $ SIGNER2_PUB_KEY=sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1
        $ SIGNER2_PRV_KEY=L5AAoEqwnHCp7WfkPcUmtUX61ppZQww345rEDCwB33jVPud4hzKJ:btc-priv-v0.0.1
        $ NETWORK_ID=mitum
        $ ./mc seal sign-fact $SIGNER2_PRV_KEY --seal data.json --network-id=$NETWORK_ID | jq

        {
            "_hint": "seal-v0.0.1",
            "hash": "GiADUurx7qVwyeu8XUNQgmNpqmtN9UDzockhLNKXzYN6",
            "body_hash": "Ci7yzpahGtXqpWs3EGfoqnmUhTgbRhdkgb2GupsJRvgB",
            "signer": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1",
            "signature": "381yXYnDDMYrZ4asLpAYgD7AHDAGMsVih11S3V2jCwNdvJJxeA96whPnth4DxXoJ3RiK8vBpvVKRvXJsPpDpZZ2GMagAmaBi",
            "signed_at": "2021-06-10T10:01:27.690429Z",
            "operations": [
                {
                    "_hint": "mitum-currency-transfers-operation-v0.0.1",
                    "hash": "AduowWC9mHTCeRp8aqN4dQxHjKGH8xdm8vqxcMj7SfUZ",
                    "fact": {
                        "_hint": "mitum-currency-transfers-operation-fact-v0.0.1",
                        "hash": "Eu1b4gr528Xy4u2sg97DsEo5uj9BuQEMjHzJxdsLgH48",
                        "token": "MjAyMS0wNi0xMFQwOTo1NDozNS44NjQwOTha",
                        "sender": "3TNoGhXH4HaXHb12PE3MhXRRNGLvcVJFfh9fUjrWFp83:mca-v0.0.1",
                        "items": [
                            {
                                "_hint": "mitum-currency-transfers-item-single-amount-v0.0.1",
                                "receiver": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
                                "amounts": [
                                    {
                                        "_hint": "mitum-currency-amount-v0.0.1",
                                        "amount": "100",
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
                            "signature": "AN1rKvtZFkx5e4NexvBSjjJkuzUj45UKau8DL2JZx5d1htnbnkmPmHnNbgwqfvUnz8KHpUR72Z9YxD4JVQhdh4JCzGv9zMDDG",
                            "signed_at": "2021-06-10T09:54:35.868223Z"
                        },
                        {
                            "_hint": "base-fact-sign-v0.0.1",
                            "signer": "sdjgo1jJ2kxAxMyBj6qZDb8okZpwzHYE8ZACgePYW4eT:btc-pub-v0.0.1",
                            "signature": "381yXZ9yqzCSzUZZUuQvU3ZMHgM9Pa5MQUo2hKGhPFW4ZuMCC3eK2iGYvx3gwQD3LCfELuUXejAQiMmeKaNAEoZVPDf1gpkE",
                            "signed_at": "2021-06-10T10:01:27.690034Z"
                        }
                    ],
                    "memo": ""
                }
            ]
        }