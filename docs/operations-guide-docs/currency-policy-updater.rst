Currency policy 업데이트
==================================================

* ``mitum-currency seal currency-policy-updater --network-id=NETWORK-ID-FLAG --feeer=STRING <privatekey> <currency-id>``
* 새로운 currency를 등록하는 경우 consensus에 참여하는 suffrage 노드들의 signature가 consensus threshold(67%)를 넘어야만 실행이 됨.
* 먼저 등록한 currency의 info를 api를 통해서 조회.

.. code-block:: sh
  
    $ curl --insecure -v https://localhost:54322/currency/MCC2 | jq
    {
    "_hint": "a016:0.0.1",
    "hint": {
        "name": "mitum-currency-currency-design",
        "hint": "a030:0.0.1"
        },
        "_embedded": {
            "_hint": "a030:0.0.1",
            "amount": {
                "_hint": "a022:0.0.1",
                "amount": "9999999999999",
                "currency": "MCC2"
            },
            "genesis_account": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1",
            "policy": {
                "_hint": "a036:0.0.1",
                "new_account_min_balance": "10",
                "feeer": {
                    "_hint": "a032:0.0.1",
                    "type": "fixed",
                    "receiver": "HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1",
                    "amount": "3"
                }
            }
        },
        "_links": {
            "currency:{currencyid}": {
                "templated": true,
                "href": "/currency/{currencyid:.*}"
            },
            "block": {
                "href": "/block/21332"
            },
            "operations": {
                "href": "/block/operation/BTxmjWqkAe9Egjds6exE28ntdTT1DrGDVJGjnjZARSfF"
            },
            "self": {
                "href": "/currency/PEN"
            }
        }
    }


* currency-policy-updater를 통해서 정책을 변경할 수 있음. 변경가능한 항목은 다음과 같음.
* feeer 정책과 --policy-new-account-min-balance


Currency-policy-updater 예제
------------------------------

* currency-id : MCC2
* 수정할 정책
* feeer : ratio
* feeer-ratio-receiver : ac0
* feeer-ratio-ratio : 0.5
* feeer-ratio-min : 3
* feeer-ratio-max : 1000
* policy-new-account-min-balance : 100
* suffrage node : n0, n1, n2, n3

.. code-block:: sh

    $ NETWORK_ID="mc; Thu 10 Sep 2020 03:23:31 PM UTC"
    $ AC0_ADDR="HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ N0_PRV=<n0 private key>
    $ N1_PRV=<n1 private key>
    $ N2_PRV=<n2 private key>
    $ N3_PRV=<n3 private key>
    $ ./bin/mc seal currency-policy-updater --network-id=$NETWORK_ID --feeer="ratio" --feeer-ratio-receiver=$AC0_ADDR \
    --feeer-ratio-ratio=0.5 --feeer-ratio-min=3 --feeer-ratio-max=1000 --policy-new-account-min-balance=100 $N0_PRV $4 \
    | ./bin/mc seal sign-fact $N1_PRV --network-id=$NETWORK_ID --seal=- \
    | ./bin/mc seal sign-fact $N2_PRV --network-id=$NETWORK_ID --seal=- \
    | ./bin/mc seal sign-fact $N3_PRV --network-id=$NETWORK_ID --seal=- \
    | ./bin/mc seal send --network-id=$NETWORK_ID $SENDER_PRV --seal=-
