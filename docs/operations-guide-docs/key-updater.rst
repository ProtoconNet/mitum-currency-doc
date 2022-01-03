.. _update key:

Update Key
==========================

keyupdater Operation
-----------------------

* This is a method of replacing the key of an account that has already been created.
* You can replace the existing registered publickey with a new publickey.
* Update to new publickey does not change *address*.

.. code-block:: sh

    $ mitum-currency seal key-updater --network-id=NETWORK-ID-FLAG <privatekey> <target> <currency> --key=KEY@...``

* KEY : "<public key>,<weight>"

Update the key of ``ac0``
--------------------------------------------------------

.. code-block:: sh

    ac0
    privatekey: KzUYFHNzxvUnZfm1ePJJ4gnLcLtMv1Tvod7Fib2sRuFmGwzm1GVbmpr
     publickey: 2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGcmpu
       address: FnuHC5HkFMpr4QABukchEeT63612gGKus3cRK3KAqK7Bmca
    
    ac1
     publickey: 247KCJyus9NYJii9rkT4R3z6GxengcwYQHwRKA6DySbiUmpu

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ NODE=https://127.0.0.1:54321
    $ AC0_PRV=KzUYFHNzxvUnZfm1ePJJ4gnLcLtMv1Tvod7Fib2sRuFmGwzm1GVbmpr
    $ AC0_PUB=2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGcmpu
    $ AC0_ADDR=FnuHC5HkFMpr4QABukchEeT63612gGKus3cRK3KAqK7Bmca
    $ AC1_PUB=247KCJyus9NYJii9rkT4R3z6GxengcwYQHwRKA6DySbiUmpu
    $ AC0_ACC_KEY=GkswusUGC22R5wmrXWB5yqFm8UN22yHLihZMkMb3z623-mca:account
    $ CURRENCY_ID=MCC
    $ ./mc seal key-updater --network-id="$NETWORK_ID" $AC0_PRV $AC0_ADDR \
        --key $AC1_PUB,100" $CURRENCY_ID | jq
        {
            "_hint": "seal-v0.0.1",
            "hash": "GvuGxKCTKWqXzgzxk3iWVGkSPAMn1nBNbAu7qgzHB8y6",
            "body_hash": "8gyB4eE7yQvneA463ZnM8LEWKDCthm8mKEFcfvAmk2pg",
            "signer": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGcmpu",
            "signature": "381yXZWCaZy3G5VLse9NCBMmJg8bPWoY4rmyAWMTRVjLKZP9WkexgJfN8EP4G2P64MPchFKtsYZ2QsNyu31rrjKQN4THtEtz",
            "signed_at": "2021-06-14T03:45:21.821896Z",
            "operations": [
                {
                    "_hint": "mitum-currency-keyupdater-operation-v0.0.1",
                    "hash": "4fFKpjDBmSrka3C3Q62fz5JYGZstZmkQTe27vgyNj4A9",
                    "fact": {
                        "_hint": "mitum-currency-keyupdater-operation-fact-v0.0.1",
                        "hash": "5yaMz2aSKS5H1wtd4YVcU4q5awbaxu7bhhswX3ss8XCb",
                        "token": "MjAyMS0wNi0xNFQwMzo0NToyMS44MTczNjNa",
                        "target": "FnuHC5HkFMpr4QABukchEeT63612gGKus3cRK3KAqK7Bmca",
                        "keys": {
                            "_hint": "mitum-currency-keys-v0.0.1",
                            "hash": "GmUiuEbsoTVLSirRWMZ2WcxT69enhEXNfskAnRJby8he",
                            "keys": [
                                {
                                    "_hint": "mitum-currency-key-v0.0.1",
                                    "weight": 100,
                                    "key": "247KCJyus9NYJii9rkT4R3z6GxengcwYQHwRKA6DySbiUmpu"
                                }
                            ],
                            "threshold": 100
                        },
                        "currency": "MCC"
                    },
                    "fact_signs": [
                        {
                            "_hint": "base-fact-sign-v0.0.1",
                            "signer": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGcmpu",
                            "signature": "AN1rKvtPv6CuiW36Q4g1wtmsGNy2Fc3ierpHgfnjXjdqjDE3wvSH293FVDYy9Yf9VTNadfMGJ38WC39hthZuGkau3vBGq7ijP",
                            "signed_at": "2021-06-14T03:45:21.821399Z"
                        }
                    ],
                    "memo": ""
                }
            ]
        }

    $ ./mc seal key-updater --network-id="$NETWORK_ID" $AC0_PRV $AC0_ADDR \
      --key $AC1_PUB,100" $CURRENCY_ID \
    | ./mc seal send --network-id="$NETWORK_ID" \
        $AC0_PRV --seal=- --node=$NODE --tls-insecure

Check the changed key of ``ac0``
--------------------------------------------------------------------------------

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | sort -g | xargs -n 1 gzcat |  grep '^{' | jq '. | select(.key == "'$AC0_ACC_KEY'") | [ "height: "+(.height|tostring),   "state_key: " + .key, "key.publickey: " + .value.value.keys.keys[0].key, "key.weight: " + (.value.value.keys.keys[0].weight|tostring), "threshold: " + (.value.value.keys.threshold|tostring)]'
    [
      "height: 3",
      "state_key: GkswusUGC22R5wmrXWB5yqFm8UN22yHLihZMkMb3z623-mca:account",
      "key.publickey: 2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGcmpu",
      "key.weight: 100",
      "threshold: 100"
    ]
    [
      "height: 104",
      "state_key: GkswusUGC22R5wmrXWB5yqFm8UN22yHLihZMkMb3z623-mca:account",
      "key.publickey: 247KCJyus9NYJii9rkT4R3z6GxengcwYQHwRKA6DySbiUmpu",
      "key.weight: 100",
      "threshold: 100"
    ]
