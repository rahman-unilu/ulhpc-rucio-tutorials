Install HAProxy
===============

To find out what version number is being offered through the official channels enter the following command.
sudo apt show haproxy

1. To install HAProxy from an outside repo, you will need to add the new repository with the following command.

.. code-block:: console
 
  sudo add-apt-repository ppa:vbernat/haproxy-1.7
  
Confirm adding the new PPA by pressing the **ENTER KEY**.


2. Update your sources list.

.. code-block:: console

  sudo apt update


3. Then install HAProxy

.. code-block:: console

  sudo apt install -y haproxy
  
Afterward, you can check the installed version number with the following command
haproxy -vOutput:

.. code-block:: console

    HA-Proxy version 1.7.8-1ppa1
    ~xenial 2017/07/09 Copyright 2000-2017 Willy Tarreau

The installation is then complete.
