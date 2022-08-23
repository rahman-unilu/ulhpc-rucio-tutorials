Uni.lu Rucio Installation Tutorials
===================================

Prerequisite:

Download rucio source file and open with code editor.

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

Contents
--------

.. toctree::

   usage
   api
