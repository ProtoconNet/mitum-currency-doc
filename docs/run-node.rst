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
    2021-03-29T09:16:55.759447Z INF dryrun? dryrun=false module=command-init
    2021-03-29T09:16:55.762494Z INF prepare to run module=command-init
    2021-03-29T09:16:55.762545Z INF prepared module=command-init
    2021-03-29T09:17:06.165294438Z INF database and block data was cleaned by force module=command-init
    2021-03-29T09:17:06.889790438Z INF genesis block created block={"hash":"EnwumZhg1eUxwjh8HARUceya9gqwzU8gK5Ecka9KjJbd","height":0} module=command-init
    2021-03-29T09:17:07.896340438Z INF stopped module=command-init
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
    2021-03-29T09:17:38.942065Z INF dryrun? dryrun=false module=command-run
    2021-03-29T09:17:38.94577Z INF prepare to run module=command-run
    2021-03-29T09:17:38.945824Z INF prepared module=command-run
    2021-03-29T09:17:46.196241322Z INF new blocks found to digest last_block=-2 last_manifest=0 module=command-run
    2021-03-29T09:17:47.396357322Z INF digested new blocks module=command-run
    2021-03-29T09:17:47.398958322Z INF trying to start http2 server for digest API bind=https://0.0.0.0:54320 module=command-run publish=https://127.0.0.1:54320
    2021-03-29T09:17:49.533142322Z INF new block stored block={"hash":"GPUqoNjhQ9GSh6p7NPuYekeJBy4K2gWkXMBGd7WwLrDB","height":1,"round":0} elapsed=38.619459 module=basic-consensus-state proposal_hash=oDhisx9UqhYGV7sujFcHKfDfL6QCpUEyn3xNerbcQpm voteproof_id=9YVXwz971QMWQerdiRNVnUJvWbwP6dqWqaNQpnhRjPq1
    2021-03-29T09:17:49.554807322Z INF block digested block=1 module=digester
    2021-03-29T09:17:51.592903322Z INF new block stored block={"hash":"Ccc79abTEQYAEeGggSnUyYY1WkyW12iBAm6PeshdzJe4","height":2,"round":0} elapsed=22.395125 module=basic-consensus-state proposal_hash=CZwieMxiCL1robs9YmeAySbQ67iQV95g1LM2Ttdj1kvb voteproof_id=Bthy5R9EW56vdPcPTYMUiMJw9tq7FAYL3oST3F1dwKGJ
    2021-03-29T09:17:51.606397322Z INF block digested block=2 module=digester
    2021-03-29T09:17:53.655096322Z INF new block stored block={"hash":"3secyQ9KYNVag2E4hhVShofM3vBYxZiBGWNq9fXEsn2H","height":3,"round":0} elapsed=25.89425 module=basic-consensus-state proposal_hash=GndqA1bQeufDmgkm8HoJ4thGn5qAmMxXgwr6Xd9PAhCr voteproof_id=2aw8Upm4pkwq5Pu16hMpcHxycPBtV4qQs1365PWc2a9E
    2021-03-29T09:17:53.667322322Z INF block digested block=3 module=digester

* If you set the log level to info, you can easily check the information of the newly created block.
* `--log` command line option can collect logs to the specific files.
* Mitum dumps huge debugging log messages, including quic(http) request message like this,

.. code-block:: sh

    2021-05-06T17:43:36.072520781Z DBG workspace/mitum/src/network/http.go:61 > request content-length=1647 content-type= duration=6.326587 headers={"X-Mitum-Encoder-Hint":["0101:0.0.1"]} host=127.0.0.1:54320 ip=127.0.0.1 method=POST module=network-quic-primitive-server proto=HTTP/3 remote=127.0.0.1:60614 req_id=c2a2li0m57f5lqgar0dg size=0 status=200 url=/seal?showme=1 user_agent="quic-go HTTP/3"


* `--network-log` command line option can collect these request messages to the specific files.

.. code-block:: sh

    $ ./mitum-currency run node \
        --log-level debug \
        --log-format json \
        --log ./mitum.log \
        --network-log ./mitum-request.log


* Multiple file can be set to `--network-log` and `--log`.
* In mitum-currency, `--network-log` option will also collect the requests log from digest API(http2) 
* `--network-log` option is only available in `node run` command.

Lookup genesis account
...........................

* You can check genesis account information through block files saved in the file system.

.. code-block:: sh

    $ find blockdata -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "8PdeEpvqfyL3uZFHRZG5PS3JngYUzFFUGPvCg29C2dBn-a000:0.0.1") | [ "height: "+(.height|tostring), "state_key: " + .key, "address: " + .value.value.address, .operations, .value.value.keys.keys, .value.value.keys.threshold]'
    [
      "height: 0",
      "state_key: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:account",
      "address: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1",
      [
        "2sQk264zRzLHUhFKHTkBQcgjJrQhZeWzymqn2SfCE3es"
      ],
      [
        {
          "_hint": "a003:0.0.1",
          "weight": 100,
          "key": "04b96826d72457a38aa9a2298c3f435f655c28a7d8e94b4e3adf772ac11e3101cbecf9e755312f8a61bd565c182f0d9d67d24f1590ddd2fef1d0af126b5bdfa5a7-0115:0.0.1"
        }
      ],
      100
    ]
    $ find blockdata -name "*-states-*" -print | xargs -n 1 zcat | jq '. | select(.key == "7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000-MCC:balance") | [ "height: "+(.height|tostring), "state_key: " + .key, "balance:" + .value.value.amount]'
    [
      "height: 0",
      "state_key: 7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000-MCC:balance",
      "balance:99999999999999999999"
    ]

* *height*, *address* of genesis account at ``0``, ``7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1`` is saved in block.
* Account information can also be checked through Digest API.

Lookup using the Digest API
---------------------------------

* The api address according to the digest setting :ref:`node configure` is https://localhost:54320.
* Check genesis account through node info

.. code-block:: sh

    $ curl --insecure -v https://localhost:54320 | jq '._embedded'
    {
        "account": {
            "_hint": "a014:0.0.1",
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
            }
        },
        "balance": "999"
    }

* Check genesis account through account information

.. code-block:: sh

    $ curl --insecure -v https://localhost:54320/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1 | jq
    {
      "_hint": "a016:0.0.1",
      "hint": {
        "hint": "a018:0.0.1",
        "name": "mitum-currency-account-value"
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
        "balance": "999",
        "height": 0,
        "previous_height": -2
      },
      "_links": {
        "operations": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations"
        },
        "operations:{offset}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}"
        },
        "operations:{offset,reverse}": {
          "templated": true,
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1/operations?offset={offset}&reverse=1"
        },
        "block": {
          "href": "/block/0"
        },
        "self": {
          "href": "/account/7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
        }
      }
    }