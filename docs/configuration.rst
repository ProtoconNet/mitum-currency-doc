.. _node configure:

Configuration
=============

* The configuration for node setting is written in YAML.

address
-------------

* Address of local node(alias for url address)

.. code-block:: yaml

    address: n0:sa-v0.0.1

genesis-operations
------------------------

* genesis-operation is a setting for the genesis operation that is executed when the network is initialized.
* genesis-operation contains the contents of the block that is initially created.
* In the currency model, information on the main currency and genesis account must be set.
* It registers the information (key, weight, threshold value) about the keys of the genesis account, and specifies the initial balance, currency ID, and fee policy of the currency to be created.

.. code-block:: yaml

    genesis-operations:
        - account-keys:
              keys:
                  - publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1
                    weight: 100
              threshold: 100
          currencies:
              - balance: "99999999999999999999"
                currency: MCC
                new-account-min-balance: "33"
          type: genesis-currencies


network
---------

* Specify the domain address or IP address of the node used in the network.
* Address to receive messages from node or client, using quic communication protocol.
* Self-signed certificates can be used to set up test node. You can use it for only test and development nodes where security is not a big concern.

.. code-block:: sh

    $ openssl genrsa -out mitum.key 4096
    $ openssl req -x509 -new -nodes -key mitum.key -sha256 -days 1024 -out mitum.crt

.. code-block:: yaml

    network:
        bind: https://0.0.0.0:54321
        url: https://127.0.0.1:54321
        cert-key: mitum.key
        cert: mitum.crt


network > rate-limit 
----------------------

* Basically API interface of internet service allows to connect from client without restriction.
* but too many requests to service does harm to the performance of service
* To maintain the service to be stable, rate limit can be applied to the API service.
* See `Rate limiting <https://en.wikipedia.org/wiki/Rate_limiting>`_
* Mitum supports quic based API service for communication within nodes(even none-suffrages)
* and Mitum-currency additionally supports http2 based API service(called digest).
* ``rate-limit`` applied to these API services.

.. code-block:: yaml

    network:
        bind: https://0.0.0.0:54321
        url: https://127.0.0.1:54321

        rate-limit:
            cache: "memory:?prefix=showme"
            preset:
                bad-nodes:
                    new-seal: 3/2m
                    blockdata: 4/m
            3.3.3.3:
                preset: bad-nodes
            4.4.4.4/24:
                preset: bad-nodes
                blockdata: 5/m
            127.0.0.1/24:
                preset: suffrage

* cache: cache for requests. At this time, supports "memory:" and "redis://<redis server>"
  
    * "memory:": memory cache
    
    * "redis://<redis server>": cached in redis server

* preset: pre defined rate limit settings. 
  
    * For Mitum, ``suffrage`` and ``world`` presets are already defined. See `launch/config/ratelimit.go <https://github.com/spikeekips/mitum/blob/master/launch/config/ratelimit.go>`_ in the `source code <https://github.com/spikeekips/mitum>`_.
    * You can make your own rate limit setting like ``bad-nodes``.

* Rules:

    * Rate-limit Settings for a specific IP
  
    * Rules consist of IP address(or IP address range), preset and detailed rate-limit settings.
  
    * The IP address can be a single value or a range of IP addresses expressed in CIDR notation.

    * example : ``3.3.3.3``, ``4.4.4.4/24``, ``127.0.0.1/24``

    * Rate limit can be set through ``preset`` and additional ``limits``.

    * ``preset`` can be pre-defined preset like ``suffrage``, ``world`` or user-defined preset like ``bad-nodes``
    
    * Additional limit such as ``blockdata: 5/m`` can be added to the preset.

    * Rules will be checked by the defined order. The upper rule will be checked first.

* detailed limit:

    * The name of the API interface for Mitum, such as ``new-seal``, used to set the limit can be found in ``RateLimitHandleMap`` (`launch/config/ratelimit.go <https://github.com/spikeekips/mitum/blob/master/launch/config/ratelimit.go>`_).

    * The name of the API interface for Mitum-currency can be found in ``RateLimitHandlerMap`` (`digest/handler.go <https://github.com/spikeekips/mitum-currency/blob/master/digest/handler.go>`_).

    * ``new-seal: 3/2m`` means ``new-seal`` interface allows 3 requests per 2 minutes to the specified IP or IP range.

    * See the `manner of time duration <https://golang.org/pkg/time/#ParseDuration>`_.

* Without any rules, by default no rate limit.
  
* A limit value less than zero means unlimited.

.. code-block::

    4.4.4.4/24:
        preset: bad-nodes
        blockdata: -1/m

* The zero limit value means that the request is blocked.

.. code-block::

    4.4.4.4/24:
        preset: bad-nodes
        blockdata: 0/m

network-id
------------

* Network id acts like an identifier that identifies a network.
* All nodes on the same network have the same network-id value.

.. code-block:: yaml

    network-id: mitum

keypair
---------

* Enter the node's private key.
* See :ref:`create keypair` to learn how to create a key pair.

.. code-block:: yaml

    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1

storage
----------

* Specify the file system path and mongodb database address of blockchain data storage.
* If blockdata setting is missing, blockdata > path is set to a folder called blockdata in the current path by default

.. code-block:: yaml

    storage:
        blockdata:
            path: ./mc-blockfs
        database:
            uri: mongodb://127.0.0.1:27017/mc

suffrage > nodes
-----------------

* Set addresses for suffrage nodes participating in consensus.
* The alias name of the local node is n0:sa-v0.0.1.
* If n0, n1, n2, n3 nodes are included in the suffrage nodes, it can be set as follows.

.. code-block:: yaml

    suffrage:
        nodes:
            - n0:sa-v0.0.1
            - n1:sa-v0.0.1
            - n2:sa-v0.0.1
            - n3:sa-v0.0.1

* If the n0 node, which is a local node, is not included in the suffrage nodes, the local node becomes a None-Suffrage node and serves only as a syncing node.
* The Syncing node does not participate in consensus and only syncs the generated block data.
* The None-suffrage node handles only the seal containing the operation.
* The None-suffrage node does not process ballots and proposals related to voting between nodes.
* When the node-suffrage node stores the operation seal, it broadcasts the seal to the suffrage nodes.
* If the None-suffrage node does not add other nodes to the suffrage node, or does not configure other suffrage nodes, operation seal cannot be processed.

.. code-block:: yaml

    suffrage:
        nodes:
            - n1:sa-v0.0.1
            - n2:sa-v0.0.1
            - n3:sa-v0.0.1

sync-interval
-----------------

* None-suffrage node periodically syncs block data.
* The default interval is 10 seconds.
* You can change the interval value through the sync-interval setting.

.. code-block:: yaml

    sync-interval: 3s

nodes
-------

* Write the address (alias for the address), public key, and url (ip address) of known nodes in the blockchain network.
* If not written, it operates as a standalone node.
* If the node is a suffrage node and the node discovery function is used, the url of the node is not required.
* However, if the node is not a suffrage node, the urls of the suffrage nodes must be included.
* Mitum nodes use CA signed certificate (public certificate) by default.
* If certificate related settings are not made in Network config, the node uses self-signed certifate.
* If other Mitum nodes use self-signed certificate, tls-insecure:true should be set to all the nodes which use self-signed certificate.

.. code-block:: yaml

    (In case of suffrage node)
    nodes:
        - address: n1:sa-v0.0.1
          publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM:btc-pub-v0.0.1
          tls-insecure: true
        - address: n2:sa-v0.0.1
          publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd:btc-pub-v0.0.1
          tls-insecure: true
        - address: n3:sa-v0.0.1
          publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb:btc-pub-v0.0.1
          tls-insecure: true

.. code-block:: yaml

    (If it is not a suffrage node)
    nodes:
        - address: n1:sa-v0.0.1
          publickey: ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM:btc-pub-v0.0.1
          url: https://127.0.0.1:54331
          tls-insecure: true
        - address: n2:sa-v0.0.1
          publickey: wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd:btc-pub-v0.0.1
          url: https://127.0.0.1:54341
          tls-insecure: true
        - address: n3:sa-v0.0.1
          publickey: vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb:btc-pub-v0.0.1
          url: https://127.0.0.1:54351
          tls-insecure: true

digest
--------

Specify the mongodb address that stores the data to be provided by the API and the IP address of the API access.

.. code-block:: yaml

    digest:
        network:
            bind: https://localhost:54320
            url: https://localhost:54320
            cert-key: mitum.key
            cert: mitum.crt

tutorial.yml (standalone node config example)
--------------------------------------------------

.. code-block:: yaml

    address: mc-node:sa-v0.0.1
    privatekey: Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA:btc-priv-v0.0.1
    storage:
        database:
            uri: mongodb://127.0.0.1:27017/mc
        blockdata:
            path: ./mc-blockfs
    network-id: mitum
    network:
        bind: https://0.0.0.0:54321
        url: https://127.0.0.1:54321
        cert-key: mitum.key
        cert: mitum.crt
    genesis-operations:
        - type: genesis-currencies
          account-keys:
              keys:
                  - publickey: rcrd3KA2wWNhKdAP8rHRzfRmgp91oR9mqopckyXRmCvG:btc-pub-v0.0.1
                    weight: 100
              threshold: 100
          currencies:
              - balance: "99999999999999999999"
                currency: MCC
                new-account-min-balance: "33"
                feeer:
                    type: fixed
                    amount: 1
    policy:
        threshold: 100
    suffrage:
        nodes: 
            - mc-node:sa-v0.0.1

    digest:
        network:
            bind: https://0.0.0.0:54320
            url: https://127.0.0.1:54320
            cert-key: mitum.key
            cert: mitum.crt