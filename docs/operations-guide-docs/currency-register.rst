.. _register currency:

Register Currency
===================

currency-register Operation
---------------------------

.. code-block:: sh

    $ ./mc seal currency-register --network-id=NETWORK-ID-FLAG --feeer=STRING --policy-new-account-min-balance=BIG <node privatekey> <currency-id> <genesis-amount> <genesis-account>

* When registering a new currency, the items that need to be set are as follows.
* genesis account: account where the issued token will be registered with new currency registration
* genesis amount: amount of newly issued tokens
* --policy-new-account-min-balance=<amount> must be set.
* feeer: The feeer can be selected from three policies {nil, fixed, ratio}.
* nil is a case where there is no fee payment, fixed is a case where a fixed amount is paid, and a ratio is a case where a payment is made in proportion to the operation amount.
* If the fee policy is fixed, you must set --feeer-fixed-receiver=<fee receiver account address> and --feeer-fixed-amount=<fee amount> accordingly.
* If the fee policy is ratio, then --feeer-ratio-receiver=<fee receiver account address> and --feeer-ratio-ratio=<fee ratio, multifly by operation amount>, --feeer-ratio-min= <minimum fee>, --feeer-ratio-max=<maximum fee> must be set.
* When registering a new currency, the signature of the suffrage nodes participating in consensus exceeds the consensus threshold (67%) to be executed.

currency-register Operation example
--------------------------------------

* genesis-account : ac1
* genesis-amount : 9999999999999
* currency-id : MCC2
* feeer : fixed
* feeer-fixed-receiver : ac1
* feeer-fixed-amount : 3
* seal sender : ac1
* suffrage node : n0, n1, n2, n3

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ AC1_ADDR="HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1"
    $ AC1_PRV="792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1"
    $ N0_PRV=<n0 private key>
    $ N1_PRV=<n1 private key>
    $ N2_PRV=<n2 private key>
    $ N3_PRV=<n3 private key>
    $ ./mc seal currency-register --network-id="$NETWORK_ID" --feeer="fixed" --feeer-fixed-receiver=$AC1_ADDR \ 
      --feeer-fixed-amount=3 --policy-new-account-min-balance=10 $N0_PRV MCC2 9999999999999 $AC1_ADDR \
      | ./mc seal sign-fact $N1_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal sign-fact $N2_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal sign-fact $N3_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal send --network-id="$NETWORK_ID" $AC1_PRV --seal=-

* Each currency has a zero account for deposit only. The zero account can be used to burn tokens.
* The zero account is an account that can only deposit token because the public key is not registered.
* The address of zero account has the same format as <currency id>-Xmca. For example, the zero account address of PEN currency is PEN-Xmca.


.. code-block:: json

    $ curl --insecure http://localhost:54320/account/PEN-Xmca | jq
    {
        "_hint": "mitum-currency-hal-v0.0.1",
        "hint": "mitum-currency-account-value-v0.0.1",
        "_embedded": {
            "_hint": "mitum-currency-account-value-v0.0.1",
            "hash": "EJvkxncxfVQNncdKZtjQTH2XuT5ECRiqSZA7LLE14zqi",
            "address": "PEN-Xmca",
            "keys": {
                "_hint": "mitum-currency-keys-v0.0.1",
                "hash": "",
                "keys": [],
                "threshold": 0
            },
            "balance": [
                {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "100000000000000000000000000",
                    "currency": "PEN"
                }
            ],
            "height": 41,
            "previous_height": 0
        },
        "_links": {
            "block": {
                "href": "/block/41"
            },
            "previous_block": {
                "href": "/block/0"
            },
            "self": {
                "href": "/account/PEN-Xmca"
            },
            "operations": {
                "href": "/account/PEN-Xmca/operations"
            },
            "operations:{offset}": {
                "href": "/account/PEN-Xmca/operations?offset={offset}",
                "templated": true
            },
            "operations:{offset,reverse}": {
                "templated": true,
                "href": "/account/PEN-Xmca/operations?offset={offset}&reverse=1"
            }
        }
    }