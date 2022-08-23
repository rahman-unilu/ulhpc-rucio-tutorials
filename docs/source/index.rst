Uni.lu Rucio Installation Tutorials
===================================

Prerequisite:

Download rucio source file and open with code editor.

Update pysftp: we have to update pysftp to use latest features of pysftp protocol


pip install pysftp


Install Ruico server

(**) Make sure you are in the project root directory (/rucio/)

(First time)
If docker is not pulled yet 
sudo docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml up -d


Enter into rucio dev server
docker exec -it dev_rucio_1 /bin/bash


Prepare and upload some demo data


tools/run_tests_docker.sh -ir


(Second time)
docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml start
docker-compose --file etc/docker/dev/docker-compose-storage-alldb.yml stop


#Use this command to restart apache server into rucio installed docker when you update code from local machine

httpd -k graceful


#Add a new user to root account with [user=user.root] and [password=123456]
rucio-admin identity add --account root --type USERPASS --email user.root@uni.lu --id user.root --password 654321@


#Add scope [scope = user.root] to a account root

rucio-admin scope add --account root --scope user.root

Contents
--------

.. toctree::

   usage
   api
