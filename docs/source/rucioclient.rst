Rucio Client
============


Batch Upload
------------

Upload script command:

Run the script to uplaod all fiels under /opt/rucio/sharedfolder/upload/files this direcotry 

.. code-block:: console

  sharedfolder/upload/run_upload_script.sh -r XRD1 -s user.root -d user.root:dataset1 -p /opt/rucio/sharedfolder/upload/files -l 10


  -r = rse (default= XRD1)
  -s = scope (default : user.root)
  -d = dataset (default: user.root:dataset1)
  -p = source path (default: (*)current directory)
  -l = batch limit (default: 10)



(***) We can add to all of our files to a dataset So that we can download all files under that dataset on single comamnd.


Batch Download
--------------

Download Script :

Downaload all the files form user.root:dataset1 into /opt/rucio/sharedfolder/download/files this direcotry 

.. code-block:: console

  sharedfolder/download/run_download_script.sh -r XRD1 -s user.root -d user.root:dataset1 -p /opt/rucio/sharedfolder/download/files -c sftp


  -r = rse (default= XRD1)
  -s = scope (default : user.root)
  -d = dataset (default: user.root:dataset1)
  -p = destination path (default: (*)current directory)
  -c = protocol (default: (‘’) Example: root, sftp)

