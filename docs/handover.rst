.. _node handover:

Node handover 
===================

Overview
----------------

Here we will explain the process of node handover.

What is handover?
---------------------
* Handover is a feature that allows a running node to be replaced without stopping.
* Nodes participating in the consensus process in the entire network may need to be replaced due to various circumstances.
* There may be cases where the program running the node needs to be updated, the node needs to be moved to another cloud service, or the node fails. In such cases, you can replace an already running node with a new one without stopping it.
* In such cases, you can replace an already running node with an alternate node without stopping it. 
* Handover is one of the key features that can support public networks in the future.

Handover scenario
----------------------------------
* Node A : the running node
* Node A-sub : the node to be replaced
* Condition: A-sub must have the same configuration as A. However, the value of network.url must be different.

Node A configuration

.. code-block:: yml

    address: A~sa-v0.0.1
    network-id: mitum
    network:
        url: https://172.17.0.1:54321
    privatekey: KyfqCLSEyfUhskZ63WtVH3m3pGgnurFHuTgkgu73Pgyjf8sxbp8R~btc-priv-v0.0.1

Node A-sub configuration

.. code-block:: yml

    address: A~sa-v0.0.1
    network-id: mitum
    network:
        url: https://172.17.0.2:54321
    privatekey: KyfqCLSEyfUhskZ63WtVH3m3pGgnurFHuTgkgu73Pgyjf8sxbp8R~btc-priv-v0.0.1

How to run
----------------------------------

* A is running as a suffrage node and wants to replace it with A-sub.
* After confirming that A is in the Consensus state, run A-sub with the node run command using the above config.
* A-sub performs synchronization by collecting previous block data and enters the syncing state.
* After confirming that the A-sub has changed to the Syncing state, execute the start-handover command on the A-sub node.

.. code-block:: sh

    $ mitum-currency node start-handover \
      "A~sa-v0.0.1" \
      "KyfqCLSEyfUhskZ63WtVH3m3pGgnurFHuTgkgu73Pgyjf8sxbp8R~btc-priv-v0.0.1" \
      "mitum" \
      "https://172.17.0.2:54321"

* When B finishes syncing, Handover starts.
* A is switched from the consensus state to the syncing state, and A-sub performs the consensus process on behalf of A.
* Other nodes in the suffrage network add A-sub as a suffrage node instead of A and proceed with the consensus process.
* Operation Seals delivered to A are delivered to other nodes

What if a start-handover is sent to A after the handover is over?
----------------------------------------------------------------------

* A replaced by A-sub is converted to the Syncing state.
* After the handover is finished, A is internally converted to the same state as A-sub before the start-handover command.
* If a start-handover command is delivered to A in this state, from then on, A attempts to replace A-sub.

How can I check that the start-handover is finished?
-----------------------------------------------------------

* When checking NodeInfo of A-sub, it is changed to CONSENSUS state
* When A's NodeInfo is checked, if it is changed to SYNCING state, handover is normally completed.