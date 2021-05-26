.. _api:

Digest API
===================

* Digest API is a service that allows nodes to search blockchain data.
* Digest API service can be used in applications such as wallet and blockchain explorer.
* API is provided through HTTP/2 network protocol.
* Response message follows `HAL <https://tools.ietf.org/html/draft-kelly-json-hal-08>`_ and is delivered in json format.
* API data storage can be set in :ref:`node configure` of Mitum currency.
* Mitum's main storage can be used or a separate database is also possible.
* TLS certificates required for HTTP/2 will randomly generate self signed certificates if the service host is localhost unless the path of the file is set separately.
* If an operation is not included in the block due to a specific problem, the cause can be checked through the response.