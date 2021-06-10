Run a node
===================

Overview
----------------

Here we will explain the process for running the node.

.. note::

  * Digest API is included in Mitum currency, so API service is provided by default.
  * Please check :ref:`node configure` for Digest setting.
  * If Digest is not set, data for API service must be processed separately.

Setting up Node
---------------------
* Please prepare tutorial.yml for :ref:`node configure` before running node.

Running the standalone node
----------------------------------

.. _node initialization:

Node init
..............

* First, the genesis block and genesis account must be created.
* The main currency is issued through the creation of the genesis block and stored in the balance of the genesis account.
* tutorial.yml : config file

.. code-block:: sh

    $ ./mc node init --log-level info ./tutorial.yml
    2021-06-10T05:13:09.232802Z INF dryrun? dryrun=false module=command-init
    2021-06-10T05:13:09.235942Z INF prepare to run module=command-init
    2021-06-10T05:13:09.236013Z INF prepared module=command-init
    2021-06-10T05:13:09.780335419Z INF genesis block created block={"hash":"6HjkXEhTNhPzUTG167jsTEany3dHebDQ5cKGNTNEzcgh","height":0} module=command-init
    2021-06-10T05:13:10.786661419Z INF stopped module=command-init
    ...
    $ echo $?
    0

.. note::

    * If already saved block data is found, an error ``environment already exists: block=0`` occurs.
    * To reset the error and ignore it, run it by adding the ``--force`` option.
    * ``$ ./mc --log-level info init ./tutorial.yml --force``

.. _make node run:

Node run
..............

* When the node is run, the blockchain's storage status and consensus participation status are changed to SYNC, JOIN, and CONSENSUS modes, and block creation starts.
* 

.. code-block:: sh

    $ ./mc node run --log-level info ./tutorial.yml 
    2021-06-10T05:14:08.225487Z INF dryrun? dryrun=false module=command-run
    2021-06-10T05:14:08.228797Z INF prepare to run module=command-run
    2021-06-10T05:14:08.228869Z INF prepared module=command-run
    2021-06-10T05:14:09.706271049Z INF new blocks found to digest last_block=-2 last_manifest=0 module=command-run
    2021-06-10T05:14:09.827980049Z INF digested new blocks module=command-run
    2021-06-10T05:14:09.828967049Z INF trying to start http2 server for digest API bind=https://localhost:54320 module=command-run publish=https://localhost:54320
    2021-06-10T05:14:11.894638049Z INF new block stored block={"hash":"CC57VpSKPozBRABPnznyMk6QY4GHn7CiSH4zSZBs8Rri","height":1,"round":0} elapsed=17.970959 module=basic-consensus-state proposal_hash=DJBgmoAJ4ef7h7iF6E3gTQ83AjWxbGDGQrmDSiQMrfya voteproof_id=BAg2HCNfBenFebuCM4P4HkDfF1off8FCBcSejdK1j7w6
    2021-06-10T05:14:11.907600049Z INF block digested block=1 module=digester

* If you set the log level to info, you can easily check the information of the newly created block.
* `--log` command line option can collect logs to the specific files.
* Mitum dumps huge debugging log messages, including quic(http) request message like this,

.. code-block:: sh

    "l":"debug","module":"http2-server","ip":"127.0.0.1","user_agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15","req_id":"c30q3kqciaejf9nj79c0","status":200,"size":2038,"duration":0.541625,"content-length":0,"content-type":"","headers":{"Accept-Language":["en-us"],"Connection":["keep-alive"],"Upgrade-Insecure-Requests":["1"]},"host":"127.0.0.1:54320","method":"GET","proto":"HTTP/1.1","remote":"127.0.0.1:55617","url":"/","t":"2021-06-10T05:23:31.030086621Z","caller":"/Users/soonkukkang/go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210609043008-298f37780037/network/http.go:61","m":"request"

* `--network-log` command line option can collect these request messages to the specific files.

.. code-block:: sh

    $ ./mc node run \
        --log-level debug \
        --log-format json \
        --log ./mitum.log \
        --network-log ./mitum-request.log \
        ./tutorial.yml

* Multiple file can be set to `--network-log` and `--log`.
* In mitum-currency, `--network-log` option will also collect the requests log from digest API(http2) 
* `--network-log` option is only available in `node run` command.

Lookup genesis account
...........................

* You can check genesis account information through block files saved in the file system.

.. code-block:: sh

    $ find blockfs -name "*-states-*" -print | xargs -n 1 gzcat | grep '^{' | jq '. | select(.key == "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca:account") | [ "height: "+(.height|tostring), "state_key: " + .key, "address: " + .value.value.address, .operations, .value.value.keys.keys, .value.value.keys.threshold]'
    [
      "height: 0",
      "state_key: GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca:account",
      "address: GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1",
      [
        "ECSDvWwxcjbEw2F3E6n6pyQXMsZn2uy7msX19XXDCYi8"
      ],
      [
        {
          "_hint": "mitum-currency-key-v0.0.1",
          "weight": 100,
          "key": "rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1"
        }
      ],
      100
    ]
    $ find blockfs -name "*-states-*" -print | xargs -n 1 gzcat | grep '^{' |jq '. | select(.key == "GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca-MCC:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance:" + .value.value.amount]'
    [
      "height: 0",
      "state_key: GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz-mca-MCC:balance",
      "balance:99999999999999999999"
    ]

* *height*, *address* of genesis account at ``0``, ``GbymDFuVmJwP4bjjyYu4L6xgBfUmdceufrMDdn4x1oz:mca-v0.0.1`` is saved in block.
* Account information can also be checked through Digest API.

Lookup using the Digest API
---------------------------------

* The api address according to the digest setting :ref:`node configure` is https://localhost:54320.

* Check genesis account through account information

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