.. _suffrage inflation:

Suffrage Inflation
===================

suffrage-inflation Operation
---------------------------

.. code-block:: sh

    $ ./mc seal suffrage-inflation --network-id=NETWORK-ID-FLAG <node privatekey> <receiver-account>,<currency-id>,<inflation-amount> 

* There are two processes to register currency in mitum-currency.
* Either through initial genesis currency creation or by registering a new currency while the network is alive.
* The registered currency has a total supply amount. The mitum-currency may increase the amount of tokens in addition to the total supply amount.
* When generate new amount, the items that need to be set are as follows.
* receiver-account: Receiving account of additionally generated tokens
* When making inflation a currency, the signature of the suffrage nodes participating in consensus exceeds the consensus threshold (67%) to be executed.

suffrage-inflation Operation example
--------------------------------------

* operation-sender-account : ac1
* receiver-account : ac2
* inflation-amount : 9999999999999
* currency-id : MCC
* seal sender : ac1
* suffrage node : n0, n1, n2, n3

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ AC1_PRV="792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be~ether-priv-v0.0.1"
    $ AC2_ADDR="DDew9vGTbLgavByTM6G28XuUdxKSAPLr8r4kw6e9YT3y~mca-v0.0.1"
    $ N0_PRV=<n0 private key>
    $ N1_PRV=<n1 private key>
    $ N2_PRV=<n2 private key>
    $ N3_PRV=<n3 private key>
    $ ./mc seal suffrage-inflation --network-id="$NETWORK_ID" $N0_PRV MCC2 9999999999999 $AC2_ADDR \
      | ./mc seal sign-fact $N1_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal sign-fact $N2_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal sign-fact $N3_PRV --network-id="$NETWORK_ID" --seal=- \
      | ./mc seal send --network-id="$NETWORK_ID" $AC1_PRV --seal=-