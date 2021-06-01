Use Cases
=====================

* 여기에 사용되는 cli 명령의 path는 :doc:`build` 에 기초하여 작성되었음.

계좌 생성한 후 생성된 계좌에서 송금
-----------------------------------

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ GENESIS_PRV="c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1"
    $ GENESIS_ADDR="7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ AC0_PUB="042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
    $ AC0_ADDR="HP6M74XVsZ8UDC7btAV2kbgQNzoDwwj1omcjfusGwK5T-a000:0.0.1"
    $ AC1_PRV=792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1
    $ AC1_PUB="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
    $ AC1_ADDR="HWXPq5mBSneSsQis6BbrNT6nvpkafuBqE6F2vgaTYfAC-a000:0.0.1"
    $ CURRENCY_ID=MCC
    $ NODE="quic://127.0.0.1:54331"
    
    # Genesis account에서 ac0 account 생성
    $ ./mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 50 --key=$AC0_PUB,100 | \
    ./mc seal send --network-id=$NETWORK_ID $GENESIS_PRV --seal=-
    
    # Genesis account에서 ac1 account 생성
    $ ./mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 50 --key=$AC1_PUB,100 | \
    ./mc seal send --network-id=$NETWORK_ID $GENESIS_PRV --seal=-

    # ac0 account에서 ac1 account로 5 송금
    ./mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $CURRENCY_ID 5 | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

multi sig 계좌 생성한 후 송금
-----------------------------

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ GENESIS_PRV="c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1"
    $ GENESIS_ADDR="7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ AC0_PUB="042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
    $ AC1_PRV=792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1
    $ AC1_PUB="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
    $ CURRENCY_ID=MCC
    $ NODE="quic://127.0.0.1:54331"

    # genesis account에서 ac0의 public key, ac1의 public key로 각각 weight 50, threshold 90인 multi sig account 생성

    $ ./mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 10000 \
    --key=$AC0_PUB,50@$AC1_PUB,50 --threshold=90 | \
    ./mc seal send --network-id=$NETWORK_ID $GENESIS_PRV --seal=- --node=$NODE

    # 생성된 multi sig account의 주소는 cli 명령으로 확인
    $ ./mc key address 90 $AC0_PUB,50 $AC1_PUB,50
    2PsqEZ27LMvAX19nVCWHyL4ctwERm5mVd7wo4DxGSUh9-a000:0.0.1

    # multi sig account에서 ac0 account로 10 송금

    $ MULTISIG_ADDR="2PsqEZ27LMvAX19nVCWHyL4ctwERm5mVd7wo4DxGSUh9-a000:0.0.1"
    $ ./mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $MULTISIG_ADDR $CURRENCY_ID 10 | \
    ./mc seal sign-fact $AC1_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

multi sig 계좌 생성 후 key update
---------------------------------

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ GENESIS_PRV="c741259e1444ce46e08c2489f3112fb8f0b9f85cb11c84ced9d948cef259ce74-0114:0.0.1"
    $ GENESIS_ADDR="7xDhv3CyDAyzdnSEFMyGV78c85wYKjDbghpghbgn6mkv-a000:0.0.1"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ AC0_PUB="042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
    $ AC1_PRV=792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1
    $ AC1_PUB="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
    $ AC2_PRV="L5TGviTiZyScUwNsZLMPu4S4gEniN2ZM3gas1tihpCDtBPxSeJph-0112:0.0.1"
    $ AC2_PUB="vV1Cy1epfu7mxpg4Gbbrd8bCikJfWyrVqNQgDWh9CQDL-0113:0.0.1"
    $ AC3_PRV="KxdGh7xzRYZEPPH6WrM5KMs22LwvV4K8hXhqPe2VdJevxCzH5TyH-0112:0.0.1"
    $ AC3_PUB="mkRPPQ1NjFe49S1uK6eY4jCdgscg7restfgQwM7A7aj4-0113:0.0.1"
    $ MULTISIG_ADDR="2PsqEZ27LMvAX19nVCWHyL4ctwERm5mVd7wo4DxGSUh9-a000:0.0.1"
    $ CURRENCY_ID=MCC
    $ NODE="quic://127.0.0.1:54331"

    # genesis account에서 ac0의 public key, ac1의 public key로 각각 weight 50, threshold 90인 multi sig account 생성

    $ ./mc seal create-account --network-id=$NETWORK_ID $GENESIS_PRV $GENESIS_ADDR $CURRENCY_ID 10000 \
    --key=$AC0_PUB,50@$AC1_PUB,50 --threshold=90 | \
    ./mc seal send --network-id=$NETWORK_ID $GENESIS_PRV --seal=- --node=$NODE

    # key update
    $ ./mc seal key-updater --network-id=$NETWORK_ID $AC0_PRV $MULTISIG_ADDR $CURRENCY_ID --key=$AC2_PUB,50@AC3_PUB,50 | \
    ./mc seal sign-fact $AC1_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

새로운 currency를 생성한 후 송금
---------------------------------

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ AC0_PUB="042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
    $ AC1_PRV=792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1
    $ AC1_PUB="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
    $ N0_PRV="Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1"
    $ N0_PUB="skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1"
    $ N0_ADDR="5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1"
    $ N1_PRV="L4R2AZVmxWUiF2FrNEFi6rHwCTdDLQ1JuQHji69SbMcmWUdNMUSF-0112:0.0.1"
    $ N1_PUB="ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1"
    $ N1_ADDR="7Zbwpruyc4pi44Y5kuycywALFDxg7vLuXmd8u9DLqYQU-a000:0.0.1"
    $ N2_PRV="L3Szj4t3w33YLsGFGeaB3v1vwae82yp5KWPcT7v1Y4WyQkAH7eCR-0112:0.0.1"
    $ N2_PUB="wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1"
    $ N2_ADDR="GQj7NN9kZ3tbiBH8UYN4VtodzLNahDKJ1aaK9DZS8HUC-a000:0.0.1"
    $ N3_PRV="KwxfBSzwevSggJz2grf8FWrjvXzrctY3WismTy6GNdJpWXe5tF5L-0112:0.0.1"
    $ N3_PUB="vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1"
    $ N3_ADDR="4tHLLLEv2pG14b92hSupWFPmfGTYMcjEMKkN3kGq7v1r-a000:0.0.1"
    $ NEW_CURRENCY_GENESIS_AMOUNT=88888888888888888888888888888888888888
    $ NEW_CURRENCY_ID=MCC2
    $ NODE="quic://127.0.0.1:54331"

    # 새로운 currency MCC2를 생성하고 ac0의 account를 genesis account로 설정함
    # currency 생성을 위해서 노드 n0, n1, n2, n3의 sign이 필요함.
    $ ./mc seal currency-register --network-id=$NETWORK_ID --feeer="fixed" --feeer-fixed-receiver=$AC0_ADDR \
    --feeer-fixed-amount=3 --policy-new-account-min-balance=10 $N0_PRV $NEW_CURRENCY_ID $NEW_CURRENCY_GENESIS_AMOUNT $AC0_ADDR | \
    ./mc seal sign-fact $N1_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N2_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N3_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

    # ac0에서 ac1으로 새로 생성된 MCC2 10을 송금
    $ ./mc seal transfer --network-id=$NETWORK_ID $AC0_PRV $AC0_ADDR $AC1_ADDR $NEW_CURRENCY_ID 10 | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

새로운 currency를 생성한 후 currency policy update
----------------------------------------------------

.. code-block:: sh

    $ NETWORK_ID="mitum"
    $ AC0_PRV="e4e236b0f02156a5c28031aa4608a299f44496be56081d09d0ef3667c33dbac3-0114:0.0.1"
    $ AC0_PUB="042f828efb3b75de4fd7d38eab7800ab212528599a3c47f3dd18658da6d8a216969f8be772c9374834b93599b1e9632f7eda536f5c6eaec582ece8d6a730b0476a-0115:0.0.1"
    $ AC1_PRV=792c971c801a8e45745938946a85b1089e61c1cdc310cf61370568bf260a29be-0114:0.0.1
    $ AC1_PUB="04a80bf7516f8b01385b680793d9d1eb3e69b8375a4ffc24a8413b13d7b5211f1aed315eec8851c391d6043fff0272b98484e5a5efa6c8815026a30029dba6c31c-0115:0.0.1"
    $ N0_PRV="Kxt22aSeFzJiDQagrvfXPWbEbrTSPsRxbYm9BhNbNJTsrbPbFnPA-0112:0.0.1"
    $ N0_PUB="skRdC6GGufQ5YLwEipjtdaL2Zsgkxo3YCjp1B6w5V4bD-0113:0.0.1"
    $ N0_ADDR="5terLZQX4fTPpjmBsjPjvwBLMY78qRWhKZ6j1kEiDNeV-a000:0.0.1"
    $ N1_PRV="L4R2AZVmxWUiF2FrNEFi6rHwCTdDLQ1JuQHji69SbMcmWUdNMUSF-0112:0.0.1"
    $ N1_PUB="ktJ4Lb6VcmjrbexhDdJBMnXPXfpGWnNijacdxD2SbvRM-0113:0.0.1"
    $ N1_ADDR="7Zbwpruyc4pi44Y5kuycywALFDxg7vLuXmd8u9DLqYQU-a000:0.0.1"
    $ N2_PRV="L3Szj4t3w33YLsGFGeaB3v1vwae82yp5KWPcT7v1Y4WyQkAH7eCR-0112:0.0.1"
    $ N2_PUB="wfVsNvKaGbzB18hwix9L3CEyk5VM8GaogdRT4fD3Z6Zd-0113:0.0.1"
    $ N2_ADDR="GQj7NN9kZ3tbiBH8UYN4VtodzLNahDKJ1aaK9DZS8HUC-a000:0.0.1"
    $ N3_PRV="KwxfBSzwevSggJz2grf8FWrjvXzrctY3WismTy6GNdJpWXe5tF5L-0112:0.0.1"
    $ N3_PUB="vAydAnFCHoYV6VDUhgToWaiVEtn5V4SXEFpSJVcTtRxb-0113:0.0.1"
    $ N3_ADDR="4tHLLLEv2pG14b92hSupWFPmfGTYMcjEMKkN3kGq7v1r-a000:0.0.1"
    $ NEW_CURRENCY_GENESIS_AMOUNT=88888888888888888888888888888888888888
    $ NEW_CURRENCY_ID=MCC2
    $ NODE="quic://127.0.0.1:54331"

    # 새로운 currency MCC2를 생성하고 ac0의 account를 genesis account로 설정함
    # currency 생성을 위해서 노드 n0, n1, n2, n3의 sign이 필요함.
    $ ./mc seal currency-register --network-id=$NETWORK_ID --feeer="fixed" --feeer-fixed-receiver=$AC0_ADDR \
    --feeer-fixed-amount=3 --policy-new-account-min-balance=10 $N0_PRV $NEW_CURRENCY_ID $NEW_CURRENCY_GENESIS_AMOUNT $AC0_ADDR | \
    ./mc seal sign-fact $N1_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N2_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N3_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE

    # currency policy를 업데이트함. currency policy 업데이트를 위해서 노드 n0, n1, n2, n3의 sign이 필요함.
    # policy 업데이트 내용 : feeer를 fixed에서 ratio로, ac1을 feeer-ratio-receiver로 수정
    $ ./mc seal currency-policy-updater --network-id=$NETWORK_ID --feeer="ratio" --feeer-ratio-receiver=$AC1_ADDR \
    --feeer-ratio-ratio=0.5 --feeer-ratio-min=3 --feeer-ratio-max=1000 --policy-new-account-min-balance=100 $N0_PRV $NEW_CURRENCY_ID | \
    ./mc seal sign-fact $N1_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N2_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal sign-fact $N3_PRV --network-id=$NETWORK_ID --seal=- | \
    ./mc seal send --network-id=$NETWORK_ID $AC0_PRV --seal=- --node=$NODE