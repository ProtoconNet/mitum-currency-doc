.. _currency policy update:

Update Currency policy
=============================

currency-policy-updater Operation
-----------------------------------

* First, get the info of the registered currency through API.
* When updating a currency policy, the signature of the suffrage nodes participating in consensus exceeds the consensus threshold (67%) to be executed.

.. code-block:: sh
  
    $ curl --insecure -v https://localhost:54320/currency/MCC2 | jq

    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-currency-design-v0.0.1",
        "_embedded": {
            "_hint": "mitum-currency-currency-design-v0.0.1",
            "amount": {
                "_hint": "mitum-currency-amount-v0.0.1",
                "amount": "9999999999999",
                "currency": "MCC2"
            },
            "genesis_account": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
            "policy": {
                "_hint": "mitum-currency-currency-policy-v0.0.1",
                "new_account_min_balance": "10",
                "feeer": {
                    "_hint": "mitum-currency-fixed-feeer-v0.0.1",
                    "type": "fixed",
                    "receiver": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
                    "amount": "3"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/currency/MCC2"
            },
            "currency:{currencyid}": {
                "templated": true,
                "href": "/currency/{currencyid:.*}"
            },
            "block": {
                "href": "/block/10"
            },
            "operations": {
                "href": "/block/operation/goNANpmA1BcnXA6TVL6AKkoxsmiaT2F5ss5zoSh7Wdt"
            }
        }
    }

* The policy that can be changed through currency-policy-updater is the fee-related policy and the minimum balance value when creating a new account.


Currency-policy-updater example
--------------------------------

* currency-id : MCC2
* Policy to be updated
* feeer : ratio
* feeer-ratio-receiver : ac1
* feeer-ratio-ratio : 0.5
* feeer-ratio-min : 3
* feeer-ratio-max : 1000
* policy-new-account-min-balance : 100
* suffrage node : n0, n1, n2, n3

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ AC1_ADDR="EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1"
    $ AC0_PRV="KzUYFHNzxvUnZfm1ePJJ4gnLcLtMv1Tvod7Fib2sRuFmGwzm1GVb:btc-priv-v0.0.1"
    $ N0_PRV=<n0 private key>
    $ N1_PRV=<n1 private key>
    $ N2_PRV=<n2 private key>
    $ N3_PRV=<n3 private key>
    $ ./mc seal currency-policy-updater --network-id="$NETWORK_ID" --feeer="ratio" --feeer-ratio-receiver=$AC1_ADDR \
    --feeer-ratio-ratio=0.5 --feeer-ratio-min=3 --feeer-ratio-max=1000 --policy-new-account-min-balance=100 $N0_PRV MCC2 \
    | ./mc seal sign-fact $N1_PRV --network-id="$NETWORK_ID" --seal=- \
    | ./mc seal sign-fact $N2_PRV --network-id="$NETWORK_ID" --seal=- \
    | ./mc seal sign-fact $N3_PRV --network-id="$NETWORK_ID" --seal=- \
    | ./mc seal send --network-id="$NETWORK_ID" $AC0_PRV --seal=-


    $ curl --insecure https://localhost:54320/currency/MCC2 | jq
    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-currency-design-v0.0.1",
        "_embedded": {
            "_hint": "mitum-currency-currency-design-v0.0.1",
            "amount": {
            "_hint": "mitum-currency-amount-v0.0.1",
            "amount": "9999999999999",
            "currency": "MCC2"
            },
            "genesis_account": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
            "policy": {
            "_hint": "mitum-currency-currency-policy-v0.0.1",
            "new_account_min_balance": "100",
            "feeer": {
                "_hint": "mitum-currency-ratio-feeer-v0.0.1",
                "type": "ratio",
                "receiver": "EuCb6BVafkV1tBLsrMqkxojkanJCM4bvmG6JFUZ4s7XL:mca-v0.0.1",
                "ratio": 0.5,
                "min": "3",
                "max": "1000"
            }
            }
        },
        "_links": {
            "currency:{currencyid}": {
            "href": "/currency/{currencyid:.*}",
            "templated": true
            },
            "block": {
            "href": "/block/13"
            },
            "operations": {
            "href": "/block/operation/3HxC5VP5Fjzent7uVVLsK44i1tp8ooH4f2Vh4c4uWM4e"
            },
            "self": {
            "href": "/currency/MCC2"
            }
        }
    }