``storage`` Command
===================

* ``storage`` command downloads, verifies, and restores block data.
* The subcommands related to ``storage`` command are as follows.
  
    * ``download`` : Download block data of specific blockheight.

    .. code-block:: sh

        $ mitum-currency storage download --tls-insecure --node=quic://127.0.0.1:54330 all 550 --save=data
    
        2021-05-26T08:56:22.485304Z INF saved file=data/000/000/000/000/000/000/550/550-manifest-0f5aaa2753d799336a84e7e1a3379a562faf3294f2a906e7109ef46703b64b23.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.515033Z INF saved file=data/000/000/000/000/000/000/550/550-operations-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.544153Z INF saved file=data/000/000/000/000/000/000/550/550-operations_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.571878Z INF saved file=data/000/000/000/000/000/000/550/550-states-0fedf0c3ccb08aea5694e04a382ca04fb1338dfc9c2c408fe6296c93c0931124.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.601769Z INF saved file=data/000/000/000/000/000/000/550/550-states_tree-d0c45c5292593853052aba6d3f410c93f6cc4473e7873ded2d623069adfc0025.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.628742Z INF saved file=data/000/000/000/000/000/000/550/550-init_voteproof-c2cea9e4821ea660973bfbf1815950879a101f1722fa15a9d76951d1a32bff39.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.658752Z INF saved file=data/000/000/000/000/000/000/550/550-accept_voteproof-5719e1186d3a55b1b13eb7adfa9e644de35283c6c631b260ef4eff23fd4fadcc.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.689224Z INF saved file=data/000/000/000/000/000/000/550/550-suffrage_info-4272fc6d391cdc22089403a75dafd10871371d8af6bd483d7d9b26e8271dfd11.jsonld.gz height=550 module=command-block-download
        2021-05-26T08:56:22.718794Z INF saved file=data/000/000/000/000/000/000/550/550-proposal-85b8e80eabfede099b1a1e5c171e32992aab94a0c1a417cc2bf8cc851f036643.jsonld.gz height=550 module=command-block-download

    * ``verify-blockdata`` : Verify blockdata in local storage.

    .. code-block:: sh

        $ mitum-currency storage verify-blockdata blockfs --network-id=mitum --verbose

        2021-05-26T08:45:15.74861211Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/cmd.go:79 > maxprocs: Leaving GOMAXPROCS=4: CPU quota undefined module=command-blockdata-verify
        2021-05-26T08:45:15.748770007Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/cmd.go:88 > flags parsed flags={"CPUProf":"mitum-cpu.pprof","EnableProfiling":false,"LogColor":false,"LogFile":null,"LogFormat":"terminal","LogLevel":"info","MemProf":"mitum-mem.pprof","NetworkID":"bWl0dW0=","Path":"/mitum/db/n0_data/blockfs","TraceProf":"mitum-trace.pprof","Verbose":true} module=command-blockdata-verify
        2021-05-26T08:45:15.748866076Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/blockdata_verify.go:38 > trying to verify blockdata module=command-blockdata-verify path=/mitum/db/n0_data/blockfs
        2021-05-26T08:45:15.750888243Z INF ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/blockdata_verify.go:107 > last height found last_height=242 module=command-blockdata-verify
        2021-05-26T08:45:15.750943528Z INF ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:53 > checking manifests module=command-blockdata-verify
        2021-05-26T08:45:15.756124734Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded heights=[-1,50] module=command-blockdata-verify
        2021-05-26T08:45:15.756409758Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked heights=[-1,50] module=command-blockdata-verify
        2021-05-26T08:45:15.761722572Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=49 heights=[50,100] module=command-blockdata-verify
        2021-05-26T08:45:15.761990104Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=49 heights=[50,100] module=command-blockdata-verify
        2021-05-26T08:45:15.765190132Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=99 heights=[100,150] module=command-blockdata-verify
        2021-05-26T08:45:15.766040741Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=99 heights=[100,150] module=command-blockdata-verify
        2021-05-26T08:45:15.770557968Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=149 heights=[150,200] module=command-blockdata-verify
        2021-05-26T08:45:15.770933787Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=149 heights=[150,200] module=command-blockdata-verify
        2021-05-26T08:45:15.77396627Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=199 heights=[200,243] module=command-blockdata-verify
        2021-05-26T08:45:15.774214677Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=199 heights=[200,243] module=command-blockdata-verify
        2021-05-26T08:45:15.774899881Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/blockdata_verify.go:253 > block data files checked height=5 module=command-blockdata-verify
        2021-05-26T08:45:15.775494443Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/blockdata_verify.go:253 > block data files checked height=98 module=command-blockdata-verify
        2021-05-26T08:45:15.776419734Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/blockdata_verify.go:253 > block data files checked height=100 module=command-blockdata-verify
        .....

    * ``verify-database`` : The database is verified by comparing it with the block data.

    .. code-block:: sh

        $ mitum-currency storage verify-database mongodb://172.31.10.67:27017/n0_mc blockfs --network-id=mitum --verbose

        2021-05-26T08:42:20.619634723Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/cmd.go:79 > maxprocs: Leaving GOMAXPROCS=4: CPU quota undefined module=command-database-verify
        2021-05-26T08:42:20.619795909Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/cmd.go:88 > flags parsed flags={"CPUProf":"mitum-cpu.pprof","EnableProfiling":false,"LogColor":false,"LogFile":null,"LogFormat":"terminal","LogLevel":"info","MemProf":"mitum-mem.pprof","NetworkID":"bWl0dW0=","Path":"/mitum/db/n0_data/blockfs","TraceProf":"mitum-trace.pprof","URI":"mongodb://172.31.10.67:27017/n0_mc","Verbose":true} module=command-database-verify
        2021-05-26T08:42:20.619911225Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process= module=process-manager process=init
        2021-05-26T08:42:20.619995329Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process=time-syncer module=process-manager process=config
        2021-05-26T08:42:20.747556897Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/util/localtime/time_sync.go:67 > started interval=120000 module=time-syncer server=time.google.com
        2021-05-26T08:42:20.750471139Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=time-syncer
        2021-05-26T08:42:20.750857313Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:359 > hook processed from=encoders hook=add_hinters module=process-manager
        2021-05-26T08:42:20.75091253Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=encoders
        2021-05-26T08:42:21.113543668Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=database
        2021-05-26T08:42:21.113673052Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:359 > hook processed from=blockdata hook=check_blockdata_path module=process-manager
        2021-05-26T08:42:21.113821044Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/database_verify.go:207 > block found block={"hash":"EjygjjRuEFvZZJzVv4mXnte66B2w6MYRvy1c7NPw5pXQ","height":159,"round":0} module=command-database-verify
        2021-05-26T08:42:21.113888587Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:359 > hook processed from=blockdata hook=check_storage module=process-manager
        2021-05-26T08:42:21.113939191Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/pm/processes.go:310 > processed from_process=init module=process-manager process=blockdata
        2021-05-26T08:42:21.113991284Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/database_verify.go:74 > trying to verify database module=command-database-verify path=/mitum/db/n0_data/blockfs uri=mongodb://172.31.10.67:27017/n0_mc
        2021-05-26T08:42:21.114039999Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/database_verify.go:100 > verifying database module=command-database-verify
        2021-05-26T08:42:21.114076714Z INF ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:53 > checking manifests module=command-database-verify
        2021-05-26T08:42:21.141941796Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded heights=[-1,50] module=command-database-verify
        2021-05-26T08:42:21.142284825Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked heights=[-1,50] module=command-database-verify
        2021-05-26T08:42:21.153351901Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=49 heights=[50,100] module=command-database-verify
        2021-05-26T08:42:21.153681595Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=49 heights=[50,100] module=command-database-verify
        2021-05-26T08:42:21.164437605Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=99 heights=[100,150] module=command-database-verify
        2021-05-26T08:42:21.164790502Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=99 heights=[100,150] module=command-database-verify
        2021-05-26T08:42:21.167414078Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:109 > manifests loaded base_height=149 heights=[150,160] module=command-database-verify
        2021-05-26T08:42:21.167544954Z DBG ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/verify_storage.go:121 > manifests checked base_height=149 heights=[150,160] module=command-database-verify
        2021-05-26T08:42:21.167594278Z INF ../go/pkg/mod/github.com/spikeekips/mitum@v0.0.0-20210526055518-21cec91c0ed4/launch/cmds/database_verify.go:105 > database verified module=command-database-verify\

    * ``clean`` : Clean storage.

    .. code-block:: sh

        $ mitum-currency storage clean node.yml

    * ``restore`` : Restore the entire database from the downloaded blockdata.