.. _seal send:

Seal Send
==================================

* Operations created in Mitum currency are transmitted in units of seals.
* Signature is required to transmit the seal. Refer to the Seal section in :ref:`Send message to node` for the part related to the keypair used for signature creation.

.. code-block:: sh

    $ mitum-currency seal send <sender privatekey> --network-id=<network id> --seal=<data file path> --node=<node quic url>

.. code-block:: sh

    $ NETWORK_ID="mc; Tue 08 Dec 2020 07:22:18 AM KST"
    $ NODE="quic://127.0.0.1:54331"
    $ AC0_PRV=L1jPsE8Sjo5QerUHJUZNRqdH1ctxTWzc1ue8Zp2mtpieNwtCKsNZ-0112:0.0.1
    $ ./bin/mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=data.json --node=$NODE
    {
      "_hint": "0151:0.0.1",
      "hash": "JBWy8z27iQdr2rxRxqBJFfNbRrBYjqqchacyvbMiwAJ4",
      "body_hash": "EQJgWRrK41GrDpEq8voJK2fNhMH6E8SBkJx6udp5g8Rs",
      "signer": "skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1",
      "signature": "AN1rKvtWsC6JzQ67xQZMgFYRbHAzxQYJ3oTSGsoZkLbWwM1Caoo5ACNrohQhBcj9G4JUGD8LFPiZsfDXKUBqY2huT8kMUpr3T",
      "signed_at": "2021-05-04T07:24:57.266723Z",
      "operations": [
        {
          "fact_signs": [
              {
                "_hint": "0150:0.0.1",
                "signer": "rd89GxTnMP91bZ1VepbkBrvB77BSQyQbquEVBy2fN1tV-0113:0.0.1",
                "signature": "AN1rKvta6ZJCcd9u4gC8p8nc9TcdcVocc3PNQs98bu2LL4Mc3V2T6br6nANDDMA6y9JEvmiW7SBWYDWkToR4pPGminekVLXco",
                "signed_at": "2021-05-04T07:24:48.832558Z"
              }
          ],
          "memo": "",
          "_hint": "a002:0.0.1",
          "hash": "ZtRM11zMQVojqpzgkRgfNUNrNf1x7rRZuGVtX7H6pHS",
          "fact": {
              "_hint": "a001:0.0.1",
              "hash": "2HWSdcdhBR42WY2bsG4khqrHsrtx5nA8MQbNgzq82bkb",
              "token": "MjAyMS0wNS0wNFQwNzoyNDo0OC44MzE5ODNa",
              "sender": "4UM4CN8MZNyv26TK84486CX5X8bu9EUYbsWz5ovRsp1M-a000:0.0.1",
              "items": [
                {
                  "_hint": "a027:0.0.1",
                  "receiver": "5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1",
                  "amounts": [
                    {
                      "_hint": "a022:0.0.1",
                      "amount": "1000",
                      "currency": "MCC"
                    }
                  ]
                }
              ]
          }
        }
      ] 
    }
    2021-05-04T07:24:57.267908Z INF trying to send seal module=command-send-seal
    2021-05-04T07:24:57.324527Z INF sent seal module=command-send-seal

* When sending to a local node for testing, an error may occur related to tls authentication.
* In this case, set --tls-insecure=true and send.

.. code-block:: sh

    $ ./bin/mc seal send --network-id=$NETWORK_ID $AC0_PRV --tls-insecure=true --seal=data.json --node=$NODE

* Whether the operation is successfully processed can be checked through the api.
* For more information, please refer to :ref:`Operation Reason`.