Pyhton Script
===================

We can upload and download using pyhton script

Upload
------

Run upload_requests.py file to upload image files of the current directory 

Update the variable before running the script:

.. code-block:: pyhton

  BASE_URL = "https://localhost:8443"
  ACCOUNT='root'
  USER_NAME='user.root'
  PASSWORD='123456'
  APP_ID='UniLuLocalMachine'
  RSE='SITE1_DISK'
  SCOPE='user.root'
  
.. code-block:: console

  python3 upload_files.py


Download
--------

Run downlaod_files.py to download all files of a RSE and scope 

Update the variable before running the script:

.. code-block:: pyhton

  BASE_URL = "https://localhost:8443"
  ACCOUNT='root'
  USER_NAME='user.root'
  PASSWORD='123456'
  APP_ID='UniLuLocalMachine'
  RSE='SITE1_DISK'
  SCOPE='user.root'
  SCHEMES = ['sftp','root']


.. code-block:: console

  python3 download_files.py
  
Batch Download
--------------
  
Run download_files_in_batch.py to download all files of a RSE and scope 

Update the variable before running the script:

.. code-block:: pyhton

  BASE_URL = "https://localhost:8443"
  ACCOUNT='root'
  USER_NAME='user.root'
  PASSWORD='123456'
  APP_ID='UniLuLocalMachine'
  RSE='SITE1_DISK'
  SCOPE='user.root'
  SCHEMES = ['sftp','root']
  CHUNK_SIZE = 2


(**) You have to define CHUNK_SIZE = 2  

.. code-block:: console

  python3 download_files_in_batch.py




