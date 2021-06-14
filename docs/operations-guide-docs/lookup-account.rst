Lookup account 
===================

Prerequisite
--------------

* *curl*
    * This is a command line tool for interacting with API. https://curl.se

* *jq*
    * This is a command line tool for parsing json response. https://stedolan.github.io/jq/

Genesis account lookup
--------------------------------------------------------------------------------

* You can lookup genesis account from local blockdata.

.. code-block:: sh

  $ AC0_ACC_KEY=381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv-mca:account
  $ find blockfs -name "*-states-*" -print | xargs -n 1 gzcat | grep '^{' | jq '. | select(.key == "'$AC0_ACC_KEY'") | [ "height: "+(.height|tostring), "state_key: " + .key, "address: " + .value.value.address, .operations, .value.value.keys.keys, .value.value.keys.threshold]'
  [
    "height: 2",
    "state_key: 381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv-mca:account",
    "address: 381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
    [
      "9mc8YEFWC27WEF3VVee1wk4ib5kvWBk1iJ41pWf27Mrc"
    ],
    [
      {
        "_hint": "mitum-currency-key-v0.0.1",
        "weight": 100,
        "key": "2Aopgs1nSzNCWLvQx5fkBJCi2uxjYBfN8TqneqFd9DzGc:btc-pub-v0.0.1"
      }
    ],
    100
  ]


* ``99999999999999999977 = 99999999999999999999 - (2 create account: 10 * 2) - (2 fee: 1 * 2)``

* Also you can lookup genesis account from digest api.

.. code-block:: sh

    $ curl --insecure https://localhost:54320/account/381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1 | jq '{_embedded}'
    {
        "_embedded": {
            "_hint": "mitum-currency-account-value-v0.0.1",
            "hash": "AHQ4ohzwm7Y9T3f8vH5LTQ2rXKfVg3eazCdyihqsWv8F",
            "address": "381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1",
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
            "balance": [
                {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "9999999999999",
                    "currency": "MCC2"
                },
                {
                    "_hint": "mitum-currency-amount-v0.0.1",
                    "amount": "50",
                    "currency": "MCC"
                }
            ],
            "height": 10,
            "previous_height": -2
        }
    }

.. note::
    * When you lookup **state** by *address* from mongodb, remove the part after ``-`` of address and use it as key.
    * ``381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv:mca-v0.0.1`` → ``381mXScfnV5mU38woCRn1VqUYqpVAoQf9fg2rXXN6iVv-mca``
    