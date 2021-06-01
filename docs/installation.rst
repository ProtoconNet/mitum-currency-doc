Installation
=============


Building Mitum Currency executable file
-----------------------------------------

After installing the Golang, please download the `Mitum Currency source code <https://github.com/spikeekips/mitum-currency>`_ .

.. code-block:: sh

    $ git clone https://github.com/spikeekips/mitum-currency.git


Build the executable file.

.. code-block:: sh
    
    $ cd mitum-currency
    $ go build -ldflags="-X 'main.Version=v0.0.1-tutorial'" -o ./mc ./main.go
    $ ./mc version
    v0.0.1