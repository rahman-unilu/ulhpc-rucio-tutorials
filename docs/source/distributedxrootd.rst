Distributed XRootD Configurataion
=================================

Distributed XRootD server
-------------------------


Olb: Open load balancers 
Basic Architecture:

A re-director node knows the XRootD protocol and accepts client calls for file access rather than serving data directly. It interacts with load balancers to find a suitable data server that can serve the client's request. 


A pure data server node known as the XRootD protocol can serve data stored on a certain file system. Each data server is potentially located on a different machine in the same local area network.

Load balancer(olb) may have the following roles:
  Manager
  Server

As a manager(olb-manager), the load balancer accepts file location requests from an XRootD redirector. Then the manager interacts with the olbs-server to check the current load and the availability of files.

On the other hand, an olb-server installed into the data server machine always pointed to an olb-manager and provide data location information to the manager. Once the actual data server is identified, the redirector redirects the client to that server. 

Note the difference between olb-server and data server. Whereas the olb-server only provides the location information, the xrootd data server really serves the actual data.


[Reference] https://osg-htc.org/docs/data/xrootd/install-storage-element/

Configuring an XRootD Server
----------------------------

