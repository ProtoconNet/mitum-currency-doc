
Command-line Options
========================

.. code-block:: shell

    $ mitum-currency --help

    Usage: mitum-currency <command>

    mitum-currency tool

    Flags:
    -h, --help    Show context-sensitive help.

    Commands:
    version                      version

    node                         node
        init                       initialize node
        <node design file>       node design file
        run                        run node
        <node design file>       node design file
        info                       node information
        <node url>               remote mitum url

    key                          key
        new                        new keypair
        verify                     verify key
        <key>                    key
        address                    generate address from key
        [<threshold>]            threshold for keys (default: 100)
        [<key> ...]              key for address (ex: "<public key>,<weight>")
        sign                       signature signing
        <privatekey>             privatekey
        <signature base>         signature base for signing

    seal                         seal
        send                       send seal to remote mitum node
        <privatekey>             privatekey for sign
        create-account             create new account
        <privatekey>             privatekey to sign operation
        <sender>                 sender address
        <currency>               currency id
        <big>                    big to send
        transfer                   transfer big
        <privatekey>             privatekey to sign operation
        <sender>                 sender address
        <receiver>               receiver address
        <currency>               currency id
        <big>                    big to send
        key-updater                update keys
        <privatekey>             privatekey to sign operation
        <target>                 target address
        <currency>               currency id
        currency-register          register new currency
        <privatekey>             privatekey to sign operation
        <currency-id>            currency id
        <genesis-amount>         genesis amount
        <genesis-account>        genesis-account address for genesis balance
        currency-policy-updater    update currency policy
        <privatekey>             privatekey to sign operation
        <currency-id>            currency id
        sign                       sign seal
        <privatekey>             sender's privatekey
        sign-fact                  sign facts of operation seal
        <privatekey>             sender's privatekey

    storage                      storage
        download                   download block data
        <data type>              data type of block data,
                                {manifest,operations,operations_tree,states,states_tree,init_voteproof,accept_voteproof,suffrage_info,proposal all}
        <height> ...             block heights of block
        verify-blockdata           verify block data
        <blockdata path>
        verify-database            verify database
        <database uri>
        <blockdata path>
        clean                      clean storage
        <node design file>       node design file
        restore                    restore
        <node design file>       node design file

    Run "mitum-currency <command> --help" for more information on a command.