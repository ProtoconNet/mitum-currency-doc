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

  $ find blockfs -name "*-states-*" -print | xargs -n 1 gzcat | grep '^{' |jq '. | select(.key == "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca-MCC:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance:" + .value.value.amount]'
  [
    "height: 0",
    "state_key: GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca-MCC:balance",
    "balance:99999999999999999999"
  ]


* ``99999999999999999977 = 99999999999999999999 - (2 create account: 10 * 2) - (2 fee: 1 * 2)``

* Also you can lookup genesis account from digest api.

.. code-block:: sh

    $ curl --insecure -v https://localhost:54320/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "name": "mitum-currency-account-value",
        "hint": "a018:0.0.1"
      },
      "_embedded": {
        "_hint": "a018:0.0.1",
        "hash": "CkNB7yu1YbAU5c8LFRV6HbFiuj9azQ3LCwuTuxMREbkd",
        "address": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
        "keys": {
          "_hint": "a004:0.0.1",
          "hash": "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv",
          "keys": [
            {
              "_hint": "a003:0.0.1",
              "weight": 100,
              "key": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1"
            }
          ],
          "threshold": 100
        },
        "balance": "99999999999999999977",
        "height": 5,
        "previous_height": 0
      },
      "_links": {
        "previous_block": {
          "href": "/block/0"
        },
        "self": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
        },
        "operations": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}",
          "templated": true
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/5"
        }
      }
    }

``ac0``
--------------------------------------------------------------------------------

* If you create account ac0, you can lookup account from local blockdata.

.. code-block:: sh

    $ find blockdata -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance: " + .value.value.amount]'
    [
      "height: 5",
      "state_key: HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:balance",
      "balance: 50"
    ]

* Check in digest api

.. code-block:: sh

    $ curl --insecure http://localhost:54320/account/GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1 | jq '{_embedded}'
    {
      "_embedded": {
        "_hint": "mitum-currency-account-value-v0.0.1",
        "hash": "6vCuuiqaYtNGfPbqfDqA234kiDoueWejd7jMs7dwvq5U",
        "address": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
        "keys": {
          "_hint": "mitum-currency-keys-v0.0.1",
          "hash": "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz",
          "keys": [
            {
              "_hint": "mitum-currency-key-v0.0.1",
              "weight": 100,
              "key": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1"
            }
          ],
          "threshold": 100
        },
        "balance": [
          {
            "_hint": "mitum-currency-amount-v0.0.1",
            "amount": "99999999999999999999",
            "currency": "MCC"
          }
        ],
        "height": 0,
        "previous_height": -2
      }
    }

.. note::
    * When you lookup **state** by *address* from mongodb, remove the part after ``-`` of address and use it as key.
    * ``GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1`` → ``GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca``
    