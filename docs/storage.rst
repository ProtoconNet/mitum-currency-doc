``storage`` Command
===================

* ``storage`` command downloads, verifies, and restores block data.
* The subcommands related to ``storage`` command are as follows.
  
    * ``download`` : Download block data of specific blockheight.

    .. code-block:: sh

        $ ./mc storage download --tls-insecure --node=quic://127.0.0.1:54330  --save=data all -- -1 0 1 2 3 4 5
    
        2021-06-08T10:50:08.018561Z INF saved file=data/000/000/000/000/000/000/0_1/-1-manifest-48cfbadd18b892bfd0a6fa230ff0c5f719bd517d37f594012aeca7244ef12599.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.018531Z INF saved file=data/000/000/000/000/000/000/000/0-manifest-307ffa78d4ce5e32e25347f5ec8ee626e44d41e55f565c2082ac00f8f128dbd9.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.058628Z INF saved file=data/000/000/000/000/000/000/0_1/-1-operations-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.068871Z INF saved file=data/000/000/000/000/000/000/000/0-operations-d17d5b941aec3c100a43e2c228bca4134473bb9c78dcf567bdd8b9e12e5cc928.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.12423Z INF saved file=data/000/000/000/000/000/000/000/0-operations_tree-45aff89f7084384fdecfac9689b75168a33f03bf6ba677ad085a6ac8fdf2bd12.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.130027Z INF saved file=data/000/000/000/000/000/000/0_1/-1-operations_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.162735Z INF saved file=data/000/000/000/000/000/000/000/0-states-73ac164e67fb49877b132aaaae2f7adf92cc237ef0e63db30f3013c283fb7100.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.172536Z INF saved file=data/000/000/000/000/000/000/0_1/-1-states-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.215233Z INF saved file=data/000/000/000/000/000/000/000/0-states_tree-7155e9c9f393943429f9341f22cba749203eaa2effd51bbbdb9b97c899cac62e.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.217385Z INF saved file=data/000/000/000/000/000/000/0_1/-1-states_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.278019Z INF saved file=data/000/000/000/000/000/000/000/0-init_voteproof-dab53369d715fc74ad750d95f1ceb859d62009165a76ea3368399da2b16bf4d7.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.287794Z INF saved file=data/000/000/000/000/000/000/0_1/-1-init_voteproof-812c550f7595c4c949d2255217a343864bdd878b09d124235d7db07758620bc7.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.319642Z INF saved file=data/000/000/000/000/000/000/000/0-accept_voteproof-09fd08050476a5d0a343154aaa0325809d721004b49cba303a58300b7415235e.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.334284Z INF saved file=data/000/000/000/000/000/000/0_1/-1-accept_voteproof-812c550f7595c4c949d2255217a343864bdd878b09d124235d7db07758620bc7.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.399426Z INF saved file=data/000/000/000/000/000/000/000/0-suffrage_info-038aa59ed7db04c96d11405336c7a2d1cb8ad6df5a18d66f8f3bf2919c6767f8.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.591648Z INF saved file=data/000/000/000/000/000/000/0_1/-1-suffrage_info-038aa59ed7db04c96d11405336c7a2d1cb8ad6df5a18d66f8f3bf2919c6767f8.jsonld.gz height=-1 module=command-block-download
        2021-06-08T10:50:08.613875Z INF saved file=data/000/000/000/000/000/000/000/0-proposal-81c03f9c912591796ae5f3dbaab85bc91d7ca4031413787abb3068c5efa78360.jsonld.gz height=0 module=command-block-download
        2021-06-08T10:50:08.750795Z INF saved file=data/000/000/000/000/000/000/0_1/-1-proposal-812c550f7595c4c949d2255217a343864bdd878b09d124235d7db07758620bc7.jsonld.gz height=-1 module=command-block-download

    * ``download map`` : Download blockdata map.
    * See :ref:`blockdata` for a detailed explanation.

    .. code-block::

        ./mc storage download map --tls-insecure --node=quic://127.0.0.1:54330 0 | jq
        {
            "_hint": "base-blockdatamap-v0.0.1",
            "hash": "DvYK11jZ8KWafAGPssypdNMRwwXwJJTKeyzTAx4JNnwc",
            "height": 10,
            "block": "AnjD39fpP6cJKVhnSfJxPfQ8sxrVwCrKhm1zWjb38dUS",
            "created_at": "2021-06-10T06:37:42.251Z",
            "items": {
                "accept_voteproof": {
                "type": "accept_voteproof",
                "checksum": "03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753",
                "url": "file:///000/000/000/000/000/000/010/10-accept_voteproof-03dd3c2ce852729ff52ec7dcd31a2a1532656fbcea12a28438c3e84c8146c753.jsonld.gz"
                },
                "init_voteproof": {
                "type": "init_voteproof",
                "checksum": "70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0",
                "url": "file:///000/000/000/000/000/000/010/10-init_voteproof-70d59dc3e84ddd06d319e9d38d68a976b09a816fbe5a5fdef42f5b80908b0fa0.jsonld.gz"
                },
                "states": {
                "type": "states",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "file:///000/000/000/000/000/000/010/10-states-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
                },
                "proposal": {
                "type": "proposal",
                "checksum": "ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465",
                "url": "file:///000/000/000/000/000/000/010/10-proposal-ccd31f6627aa3cc6e9768b318f8cfd8e7f371b907f329fb89d692c7aea2ef465.jsonld.gz"
                },
                "suffrage_info": {
                "type": "suffrage_info",
                "checksum": "f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e",
                "url": "file:///000/000/000/000/000/000/010/10-suffrage_info-f8955c57fb4a7dc48e71973af01852008c76ae4bb5487f8d6fccebcc10e5412e.jsonld.gz"
                },
                "manifest": {
                "type": "manifest",
                "checksum": "1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880",
                "url": "file:///000/000/000/000/000/000/010/10-manifest-1f21552b0d7a11c0397c7429849a0f611d9681f70cecd5165e21fcbd5276a880.jsonld.gz"
                },
                "operations": {
                "type": "operations",
                "checksum": "d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59",
                "url": "file:///000/000/000/000/000/000/010/10-operations-d890f3ba40375a6b2d331883907dc0a9ca980ce45f7d5dcaca9087278c0b6d59.jsonld.gz"
                },
                "states_tree": {
                "type": "states_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "file:///000/000/000/000/000/000/010/10-states_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
                },
                "operations_tree": {
                "type": "operations_tree",
                "checksum": "1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26",
                "url": "file:///000/000/000/000/000/000/010/10-operations_tree-1f9877aebf8854fd42154c6e6479ff6a3e379b2762c65995c80f3dff2a357a26.jsonld.gz"
                }
            },
            "writer": "blockdata-writer-v0.0.1"
        }

    * ``verify-blockdata`` : Verify blockdata in local storage.

    .. code-block:: sh

        $ ./mc storage verify-blockdata data --network-id=mitum --verbose

        2021-06-08T10:52:03.249204Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/cmd.go:86 > maxprocs: Leaving GOMAXPROCS=8: CPU quota undefined module=command-blockdata-verify
        2021-06-08T10:52:03.250015Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/cmd.go:95 > flags parsed flags={"CPUProf":"mitum-cpu.pprof","EnableProfiling":false,"LogColor":false,"LogFile":null,"LogFormat":"terminal","LogLevel":"info","LogOutput":{},"MemProf":"mitum-mem.pprof","NetworkID":"bWl0dW0=","Path":"data","TraceProf":"mitum-trace.pprof","Verbose":true} module=command-blockdata-verify
        2021-06-08T10:52:03.250188Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:38 > trying to verify blockdata module=command-blockdata-verify path=data
        2021-06-08T10:52:03.250315Z INF ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:107 > last height found last_height=5 module=command-blockdata-verify
        2021-06-08T10:52:03.250607Z INF ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:53 > checking manifests module=command-blockdata-verify
        2021-06-08T10:52:03.255675Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:109 > manifests loaded heights=[-1,6] module=command-blockdata-verify
        2021-06-08T10:52:03.255766Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:121 > manifests checked heights=[-1,6] module=command-blockdata-verify
        2021-06-08T10:52:03.258293Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=0 module=command-blockdata-verify
        2021-06-08T10:52:03.257947Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=1 module=command-blockdata-verify
        2021-06-08T10:52:03.259131Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=4 module=command-blockdata-verify
        2021-06-08T10:52:03.257772Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=5 module=command-blockdata-verify
        2021-06-08T10:52:03.260384Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=2 module=command-blockdata-verify
        2021-06-08T10:52:03.260419Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=-1 module=command-blockdata-verify
        2021-06-08T10:52:03.260606Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:257 > block data files checked height=3 module=command-blockdata-verify
        2021-06-08T10:52:03.274069Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=-1 module=command-blockdata-verify
        2021-06-08T10:52:03.279165Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=3 module=command-blockdata-verify
        2021-06-08T10:52:03.279179Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=2 module=command-blockdata-verify
        2021-06-08T10:52:03.279223Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=1 module=command-blockdata-verify
        2021-06-08T10:52:03.279267Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=4 module=command-blockdata-verify
        2021-06-08T10:52:03.279344Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=5 module=command-blockdata-verify
        2021-06-08T10:52:03.281481Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:187 > block checked height=0 module=command-blockdata-verify
        2021-06-08T10:52:03.281569Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/blockdata_verify.go:87 > blockdata verified module=command-blockdata-verify
        .....

    * ``verify-database`` : The database is verified by comparing it with the block data.

    .. code-block:: sh

        $ ./mc storage verify-database mongodb://127.0.0.1:27017/n0_mc blockfs --network-id=mitum --verbose

        2021-06-08T10:56:20.879671Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/cmd.go:86 > maxprocs: Leaving GOMAXPROCS=8: CPU quota undefined module=command-database-verify
        2021-06-08T10:56:20.879921Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/cmd.go:95 > flags parsed flags={"CPUProf":"mitum-cpu.pprof","EnableProfiling":false,"LogColor":false,"LogFile":null,"LogFormat":"terminal","LogLevel":"info","LogOutput":{},"MemProf":"mitum-mem.pprof","NetworkID":"bWl0dW0=","Path":"data","TraceProf":"mitum-trace.pprof","URI":"mongodb://127.0.0.1:27017/mc","Verbose":true} module=command-database-verify
        2021-06-08T10:56:20.880018Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process= module=process-manager process=init
        2021-06-08T10:56:20.880066Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process=time-syncer module=process-manager process=config
        2021-06-08T10:56:21.038454Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/util/localtime/time_sync.go:67 > started interval=120000 module=time-syncer server=time.google.com
        2021-06-08T10:56:21.042330408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=time-syncer
        2021-06-08T10:56:21.042835408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:359 > hook processed from=encoders hook=add_hinters module=process-manager
        2021-06-08T10:56:21.042884408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=encoders
        2021-06-08T10:56:21.203404408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=database
        2021-06-08T10:56:21.203608408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:359 > hook processed from=blockdata hook=check_blockdata_path module=process-manager
        2021-06-08T10:56:21.203899408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/database_verify.go:207 > block found block={"hash":"CzF6t6ePyBaz6RnSjw6YRhwKsxA5sRnhHwQJvK8xVgMR","height":0,"round":0} module=command-database-verify
        2021-06-08T10:56:21.204001408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:359 > hook processed from=blockdata hook=check_storage module=process-manager
        2021-06-08T10:56:21.204054408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=blockdata
        2021-06-08T10:56:21.204357408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/database_verify.go:74 > trying to verify database module=command-database-verify path=data uri=mongodb://127.0.0.1:27017/mc
        2021-06-08T10:56:21.204424408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/database_verify.go:100 > verifying database module=command-database-verify
        2021-06-08T10:56:21.204941408Z INF ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:53 > checking manifests module=command-database-verify
        2021-06-08T10:56:21.210215408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:109 > manifests loaded heights=[-1,1] module=command-database-verify
        2021-06-08T10:56:21.210355408Z DBG ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/verify_storage.go:121 > manifests checked heights=[-1,1] module=command-database-verify
        2021-06-08T10:56:21.210456408Z INF ../../../../pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210605063447-f720096b150d/launch/cmds/database_verify.go:105 > database verified module=command-database-verify

    * ``clean`` : Clean storage.

    .. code-block:: sh

        $ ./mc storage clean node.yml

    * ``restore`` : Restore the entire database from the downloaded blockdata.
    * Check if the network id in the settings of the yml file is the same as the network id of the downloaded node.

    .. code-block:: sh

        $ ./mc storage restore node.yml

        2021-06-08T11:00:34.304594Z INF prepare to run module=command-restore
        2021-06-08T11:00:34.304656Z INF prepared module=command-restore
        2021-06-08T11:00:34.743477729Z INF block restored height=-1 module=command-restore
        2021-06-08T11:00:34.828859729Z INF block restored height=0 module=command-restore
        2021-06-08T11:00:34.829060729Z INF restored module=command-restore
        2021-06-08T11:00:35.833206729Z INF stopped module=command-restore

    * ``set-blockdatamaps`` :  Update the multiple BlockDataMaps
    * See :ref:`blockdata` for a detailed explanation.
