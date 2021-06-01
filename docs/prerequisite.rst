Prerequisite
============

Database
------------------
| Mitum currency uses mongodb as its main storage engine.
| To run the Mitum currency node, you need to prepare mongodb first.

* MongoDB
    - Installation
        - `Manual Installation Guide <https://docs.mongodb.com/manual/installation/>`_
        - Using `docker container <https://hub.docker.com/_/mongo>`_
        - ``$ docker run --name mc-test-mongo-27017 -it -p 27017:27017 -d mongo``
    - Setup
        * For more information on db setup, see :ref:`node configure` .


Golang
-------------
| Mitum currency is developed using the programming language `Go <https://golang.org>`_.
| To create an executable binary, you need to build it from the source code.
| We do not provide detailed instructions for installing the Go language here.
| For more information, refer to `How to Install Go <https://golang.org/doc/install>`_.
| You must have the Golang installed with at least version 1.16 to build Mitum currency. 