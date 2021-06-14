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
    