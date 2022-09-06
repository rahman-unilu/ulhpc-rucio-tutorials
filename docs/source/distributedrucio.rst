Distributed Rucio server configuration
======================================

Prerequisite:

1. Clone source code from the git repo.
	https://gitlab.uni.lu/omarcu/rucio.git
	
.. code-block:: console
	
	git clone https://gitlab.uni.lu/omarcu/rucio.git
	
Switch to branch xrood-protocol

2. Check docker version 

.. code-block:: console

   sudo docker --version 

If docker is not installed, install the docker and docker-compose:

.. code-block:: console

   sudo apt install docker.io
   sudo apt install docker-compose


Install multiple rucio server
---------------------------

For distrbuted system we have install multilple rucio servers.

For installing first server, database and RSE server we can follow the following instructions 

(**)Make sure you are in the project root directory (/rucio/)

Now we have to update ip for databse server, so that multiple rucio can access the same databse.

.. code-block:: console

   vi docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml up -d

.. image:: server1_config.png
   :width: 500



And for instaling second rucio server we can run the command 

(**) Make sure you are in the project root directory (/rucio/)

.. code-block:: console

   sudo docker-compose --file etc/docker/dev/docker-compose-only-server.yml up -d
   
 

