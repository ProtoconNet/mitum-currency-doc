.. _technical spec:

Mitum technical spec
=======================

* Mitum (blockchain core framework) uses *ISAAC+* consensus protocol based on *PBFT*.
* The network transport protocol is `quic <https://en.wikipedia.org/wiki/QUIC>`_ (based on udp).
* Gossip-Based Node Discovery Protocol.
* The main storage engine of the blockchain uses *mongodb* and the local file system is used for block storage.
* **parallel** operation processing
* main hash algorithm: `Keccak <https://keccak.team>`_ 256, `SHA-3 <https://pkg.go.dev/golang.org/x/crypto/sha3#New256>`_
* supports multiple hash algorithm: *keccak 256*, *keccak 512*, raw bytes.
* supports multiple keypair: *btc*, *ethereum*, *stellar*.
* supports multiple message serialization format: *json*, *bson*
* small amount of code.
* *json* logging