The Livepeer Node
===============================

The Livepeer node is a command line executable called ``livepeer``  that connects to other nodes on the Livepeer network and speaks the Livepeer protocol. It comes with an accompanying command line interface (CLI) called ``livepeer_cli`` which makes it easy to take a number of actions on the network.

Installation
------------------
You can download precompiled binaries, or you can build the latest version from source.

Download Executables
^^^^^^^^^^^^^^^^^^^^^^^

Follow the instructions on :doc:`getting_started` to download the binaries for your platform and set their permissions.


Building from Source
^^^^^^^^^^^^^^^^^^^^^^

The latest instructions for building the `go-livepeer project`_ can be found on `Github`_.

.. _go-livepeer project: https://github.com/livepeer/go-livepeer
.. _Github: https://github.com/livepeer/go-livepeer


Running a node
-------------------------------

.. _offchain:

In offchain mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using offchain mode does not require syncing with the Ethereum blockchain. Start a node in offchain mode with the command::

  $ livepeer --offchain --bootnode

The ``--bootnode`` flag tells this node not to look to connect to a remote boot node in order to discover other peers. Instead, this role itself will play the role of boot node, that other peers can connect to.

You are now running a node, and can use it to develop and test Livepeer locally, or even use it as the basis to begin forming a `private network`_.

.. _testnet:

Running a node on the Livepeer Testnet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Livepeer testnet is a set of nodes that are available syncing with a private Ethereum blockchain. The homepage for the testnet is available at http://eth-testnet.livepeer.org/.

Install and start Geth
~~~~~~~~~~~~~~~~~~~~~~~~~

Geth is the Ethereum client which is required to sync the testnet blockchain. The instructions for installing geth are available on the `Ethereum installation guide`_. Generally this is just downloading a binary file for your platform.

The "connect yourself" tab on the `Testnet Homepage`_ provides instructions for how to initialize Geth and launch it. It can be summarized as:

* Create a geth data directory. For example::

  $ mkdir ~/.lpGeth
  
  We recommend creating a new directory even if you already have one, so the Livepeer testing data will be stored separately.

* Download the genesis json `lptestnet.json`_. It can be saved anywhere. It'll just be used once for the next step

* Initialize your local geth node with testnet genesis block. For example::

  $ geth --datadir ~/.lpGeth init lptestnet.json
  
.. note:: Depending on your geth version, you may see a complaint about 'genesis.number' related to your .json file. To fix the issue, delete the "number" field in the json.

* Start geth with the network id ``858585`` and the Livepeer testnet bootnode. For example::

    $geth --datadir ~/.lpGeth --networkid 858585 --bootnodes "enode://080ebca2373d15762c29ca8d85ddc848f10a7ffc745f7110cacba4694728325d645292cb512d7168323bd0af1650fca825ff54c8dba20aec8878498fae3ff3c6@18.221.67.74:30303"
    
  Now the geth node should be running, and it should soon start downloading blocks.

.. note: The actual values for networkid and bootnodes flags should be taken from the "Connect Yourself" tab on the `Testnet Homepage`_.

.. _Ethereum installation guide: https://github.com/ethereum/go-ethereum/wiki/Building-Ethereum
.. _Testnet Homepage: http://eth-testnet.livepeer.org/
.. _lptestnet.json: http://eth-testnet.livepeer.org/lptestnet.json

.. _run livepeer:

Run Livepeer
~~~~~~~~~~~~~~~~~~~~~~~~

Make sure that you have gone through the installation steps for both Livepeer, and its dependencies ffmpeg and geth. Make sure geth is running. Now you can start Livepeer::

  $ livepeer -testnet

In a separate terminal window, run livepeer_cli::

  $ livepeer_cli

Livepeer CLI will print out your account address, ETH balance, Livepeer token balance, and more info. It should present an array of options for interacting with Livepeer::

  What would you like to do? (default = stats)
  1. Get node status
  2. Deposit token
  3. Broadcast video
  4. Stream video
  5. Set broadcast config
  6. Bond
  7. Unbond
  8. Withdraw bond
  9. Get test Livepeer Token
  10. Get test Ether
  11. List registered transcoders


The testnet contains faucets for providing you with test ETH and test Livepeer Token (LPT), which you will need to take other actions in Livepeer.

* Get some test eth from the eth faucet from http://eth-testnet.livepeer.org/. Make sure to use the Eth account address printed out above in ``livepeer_cli``. Remember to add 0x as a prefix to address, if not present.

  * You can check that the request is successful by going to ``livepeer_cli`` and selecting Get node status. You should see a positive Eth balance.

* Now get some test Livepeer tokens. Pick Get test Livepeer Token.

  * You can check that the request is successful by going to ``livepeer_cli`` and selecting Get node status. You should see your Token balance go up.

Now that you have Livepeer token and ETH you can use them broadcast, bond and delegate, or even become a transcoding node:

* :doc:`broadcasting`
  
* :doc:`bonding_and_delegation`
  
* :doc:`transcoding`

.. _private network:

Running a node on a private network
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^