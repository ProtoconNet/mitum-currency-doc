.. _update key:

Update Key
==========================

keyupdater Operation
-----------------------

* This is a method of replacing the key of an account that has already been created.
* You can replace the existing registered publickey with a new publickey.
* Update to new publickey does not change *address*.

``` mitum-currency seal key-updater --network-id=NETWORK-ID-FLAG <privatekey> <target> <currency> --key=KEY@...```

* KEY : "<public key>,<weight>"

Update the key of ``ac0``
--------------------------------------------------------

.. code-block:: sh

    ac0
    privatekey: L1jPsE8Sjo5QerUHJUZNRqdH1ctxTWzc1ue8Zp2mtpieNwtCKsNZ-0112:0.0.1
     publickey: rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1
       address: 4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1
     



.. code-block:: sh

    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ AC0_PRV=L1jPsE8Sjo5QerUHJUZNRqdH1ctxTWzc1ue8Zp2mtpieNwtCKsNZ-0112:0.0.1
    $ AC0_PUB=rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1
    $ AC0_ADDR=4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1
    $ ./bin/mc seal key-updater --network-id=$NETWORK_ID $AC0_PRV 
        "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1-a000:0.0.1" \
        --key "047cccc413bc0fbabb92da3fd01808252d29d99c8201df0dc6dbd3b972943f9523ac4144abe9e1bebf9a02c1a04aef5dcc5ded1a4c395dfb1aa23251e293f71efb-0115:0.0.1,100" | jq
    {
      "_hint": "0151:0.0.1",
      "hash": "AHCwTPZbY1zXQJasEVXJLGqjxf89rcnFrciW7ebyYYDf",
      "body_hash": "4xonwJQfoxwWTvZGbAYgntiCMYQZLtCg9rGgX9G4mPp5",
      "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
      "signature": "vJ4hqdZRiJiXMS5tZyigZjLscdHbv3GDph9DuJYHjmHWVDmqaVwGrGSqEhtUWF9LKDT6ggBPzCq6qYM4zVoQpyCKD7u",
      "signed_at": "2020-09-16T13:35:54.926927425+09:00",
      "operations": [
        {
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
              "signature": "5BpRZ5TRt2qUdXwSUPhMDj1mbyY12R2VYz8YZYAjWUYTBZqkzLprdKHVJe3VnpBwub1Pj7HNq3EQvmXSQ3EyyA7BvziC4",
              "signed_at": "2020-09-16T13:35:54.926914596+09:00"
            }
          ],
          "memo": "",
          "_hint": "a010:0.0.1",
          "hash": "Hn6MMTnRpzoYKpcvxxULJSE8y3LF6V3CmrV7DZs2pLjz",
          "fact": {
            "_hint": "a009:0.0.1",
            "hash": "8zd8EVPRBuxFsXSf1WgmmCZQy6qDHjEhEX4CLnd4JbAo",
            "token": "MjAyMC0wOS0xNlQxMzozNTo1NC45MjY2NTk2NDUrMDk6MDA=",
            "target": "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1-a000:0.0.1",
            "keys": {
              "_hint": "a004:0.0.1",
              "hash": "CHH7LQZnaerpKewx5Tz9zPL7g7xnYbpmBQ1HrrS8Bt83",
              "keys": [
                {
                  "_hint": "a003:0.0.1",
                  "weight": 100,
                  "key": "047cccc413bc0fbabb92da3fd01808252d29d99c8201df0dc6dbd3b972943f9523ac4144abe9e1bebf9a02c1a04aef5dcc5ded1a4c395dfb1aa23251e293f71efb-0115:0.0.1"
                }
              ],
              "threshold": 100
            }
          }
        }
      ]
    }

    $ ./bin/mc seal key-updater --network-id="mc; Thu 10 Sep 2020 03:23:31 PM UTC" \
        "e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1" \
        "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1-a000:0.0.1" \
        --key "047cccc413bc0fbabb92da3fd01808252d29d99c8201df0dc6dbd3b972943f9523ac4144abe9e1bebf9a02c1a04aef5dcc5ded1a4c395dfb1aa23251e293f71efb-0115:0.0.1,100" | \
    ./bin/mc seal send --network-id="mc; Thu 10 Sep 2020 03:23:31 PM UTC" \
        "c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1" \
        --seal=-

Check the changed key of ``ac0``
--------------------------------------------------------------------------------

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | sort -g | xargs -n 1 zcat | jq '. | select(.key == "EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1:account") | [ "height: "+(.height|tostring),   "state_key: " + .key, "key.publickey: " + .value.value.keys.keys[0].key, "key.weight: " + (.value.value.keys.keys[0].weight|tostring), "threshold: " + (.value.value.keys.threshold|tostring)]'
    [
      "height: 5",
      "state_key: EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1:account",
      "key.publickey: 042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
      "key.weight: 100",
      "threshold: 100"
    ]
    [
      "height: 24",
      "state_key: EinT1E7FADZN1y4WrQcWzyfM2UnG6FmaGQM2Q4qyJVn1:account",
      "key.publickey: 047cccc413bc0fbabb92da3fd01808252d29d99c8201df0dc6dbd3b972943f9523ac4144abe9e1bebf9a02c1a04aef5dcc5ded1a4c395dfb1aa23251e293f71efb-0115:0.0.1",
      "key.weight: 100",
      "threshold: 100"
    ]
