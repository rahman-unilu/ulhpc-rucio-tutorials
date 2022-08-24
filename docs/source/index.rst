Uni.lu Rucio Installation Tutorials
===================================

Prerequisite:


Clone source code from the git repo.
	https://gitlab.uni.lu/omarcu/rucio.git
	
.. code-block:: console
	
	git clone https://gitlab.uni.lu/omarcu/rucio.git
	
Switch to branch xrood-protocol

Check docker version 

.. code-block:: console

   sudo docker --version 

If docker is not installed, install the docker and docker-compose:

.. code-block:: console

   sudo apt install docker.io
   sudo apt install docker-compose


Update pysftp: we have to update pysftp to use latest features of pysftp protocol

.. code-block:: console

   pip install pysftp


Install Ruico server

(**) Make sure you are in the project root directory (/rucio/)



(First time)
If docker is not pulled yet 

.. code-block:: console

   sudo docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml up -d


Enter into rucio dev server

.. code-block:: console

   docker exec -it dev_rucio_1 /bin/bash

   


Prepare and upload some demo data

.. code-block:: console

   tools/run_tests_docker.sh -ir


(Second time)

.. code-block:: console

   docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml start
   docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml stop


#Use this command to restart apache server into rucio installed docker when you update code from local machine

.. code-block:: console

   httpd -k graceful


#Add a new user to root account with [user=user.root] and [password=123456]

.. code-block:: console

   rucio-admin identity add --account root --type USERPASS --email user.root@uni.lu --id user.root --password 654321@


#Add scope [scope = user.root] to a account root

.. code-block:: console

   rucio-admin scope add --account root --scope user.root

#Add some dataset [scope:datasetName]

.. code-block:: console

   rucio add-dataset user.root:dataset1
   rucio add-dataset user.root:dataset2


#Add some container [scope:containerName]

.. code-block:: console

   rucio add-container user.root:container1
   rucio add-container user.root:container2



# Then, create the RSEs [ SITE1_DISK, SITE2_DISK ] 

.. code-block:: console

   rucio-admin rse add SITE1_DISK
   rucio-admin rse add SITE2_DISK


# Add the protocol definitions for the rucio storage servers (RSE)

(***) Use --impl rucio.rse.protocols.sftp_byte_file.Default for impl PCOG custom sftp protocol to support upload byte file and download byte file

(***) Add credentials of sftp server as 
--extended-attributes-json '{"credentials": {"username": "demo", "password": "demo"}}' 

.. code-block:: console

   rucio-admin rse add-protocol --hostname 127.0.0.1 --scheme sftp --prefix /sftp/rucio --port 22 --impl rucio.rse.protocols.sftp_byte_file.Default --domain-json '{"wan": {"read": 1, "write": 1, "delete": 1, "third_party_copy_read": 1, "third_party_copy_write": 1}, "lan": {"read": 1, "write": 1, "delete": 1}}' --extended-attributes-json '{"credentials": {"username": "demo", "password": "demo"}}' SITE1_DISK

.. code-block:: console

   rucio-admin rse add-protocol --hostname 127.0.0.1 --scheme sftp --prefix /sftp/rucio --port 22 --impl rucio.rse.protocols.sftp_byte_file.Default --domain-json '{"wan": {"read": 1, "write": 1, "delete": 1, "third_party_copy_read": 1, "third_party_copy_write": 1}, "lan": {"read": 1, "write": 1, "delete": 1}}' --extended-attributes-json '{"credentials": {"username": "demo", "password": "demo"}}' SITE2_DISK


Check your added protocol of RSE[SITE1_DISK] :

.. code-block:: console
   rucio-admin rse info SITE1_DISK
   rucio-admin rse info SITE2_DISK



# SET Indefinite limits for RSE[SITE1_DISK] of an account[root]   (-1, 1GB, 100GB, 100000)

.. code-block:: console

   rucio-admin account set-limits root SITE1_DISK -1
   rucio-admin account set-limits root SITE2_DISK -1



Contents
--------

.. toctree::
   
   self
   api
   script
   rucioclient
   distributedxrootd
   
