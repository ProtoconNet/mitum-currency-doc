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

    $ AC0_PRV=e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1
    $ AC0_ADDR=HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1
    $ AC1_ADDR=HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1
    $ CURRENCY_ID=MCC
    $ NETWORK_ID="mitum"
    $ ./mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq
    {
      "_hint": "0151:0.0.1",
      "hash": "ACSP5cdJRTz4YFg72sAxsTzgECwNsJ9J2J3DtY7a2uYe",
      "body_hash": "G9C8x27G777hsTMXd1BcoMBqWyhnh7QX3H7jwxfmNFt3",
      "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
      "signature": "5BpRZ6YGtewJnaRw7mpK3DKJraAHTLrVY7Yuy1qy7Vs9bpLT2kbkZuKjG6Hr7TCHKahJunbqBKQGRenAGDktfYixQsYdY",
      "signed_at": "2020-09-16T13:31:12.203767242+09:00",
      "operations": [
        {
          "fact": {
            "_hint": "a001:0.0.1",
            "hash": "AVQivpcsT1gApMQZLTV1p89cVK3hZkJEzr26qxdxsbnW",
            "token": "MjAyMC0wOS0xNlQxMzozMToxMi4yMDM1NjExNDcrMDk6MDA=",
            "sender": "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1",
            "items": [
              {
                "receiver": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1",
                "amount": "3"
              }
            ]
          },
          "fact_signs": [
            {
              "_hint": "0150:0.0.1",
              "signer": "042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1",
              "signature": "5BpRZ96xDRW3QzpigYNPthKDJgEu2488bseE79G2YoKMsgV7jFm3SzWXciBgZdAAmFzcJ7R3EJvRkm4FTfekRCjuXeTFe",
              "signed_at": "2020-09-16T13:31:12.20375494+09:00"
            }
          ],
          "memo": "",
          "_hint": "a002:0.0.1",
          "hash": "JAgPABZ6vX8icHDQTJEyNXe5KzY3c6jF4UmCRTVQo24y"
        }
      ]
    }

    $ ./mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 3 | jq \
      ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=-

* Whether the operation is successfully processed can be checked through the api.
* For more information, please refer to :ref:`Operation Reason`.