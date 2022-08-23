API
===

Upload And Download (Using Postman: API call)

Upload
------

Auth Token:

For api calling first we have to get token uging auth api
url = "https://localhost:8443/auth/userpass"

.. code-block:: javascript

   payload={}
   headers = {
    'X-Rucio-Account': 'root',
    'X-Rucio-Username': 'user.root',
    'X-Rucio-Password': '123456',
    'X-Rucio-AppID': 'postman'
   }
   response = requests.request("GET", url, headers=headers, data=payload)

Response Headers

.. code-block:: javascript

   X-Rucio-Auth-Token – The authentication token
After getting token we can use it to next api calling


Upload file using upload api calling 

.. code-block:: javascript

   {{API_BASE_URL}}/upload/{{account}}/{{rse}}/{{scope}}

 

.. code-block:: javascript

   url = "https://localhost:8443/upload/root/SITE1_DISK/user.root"

   payload={}
   files=[
    ('file',('n7.jpg',open('/home/pcog/Downloads/nature/n7.jpg','rb'),'image/*))
   ]
   headers = {
    'x-rucio-auth-token': ‘Token’
   }

   response = requests.request("POST", url, headers=headers, data=payload, files=files)





Download
--------


For downloading


3.a Get all dids by scope
{{API_BASE_URL}}/dids/{{scope}}

.. code-block:: javascript

   url = "https://localhost:8443/dids/user.root"

   payload={}
   headers = {
    'x-rucio-auth-token': 'token'
   }
   response = requests.request("GET", url, headers=headers, data=payload)

Response :

.. code-block:: javascript
   {
      "scope": "user.root",
      "name": "1.png",
      "type": "FILE",
      "parent": null,
      "level": 0,
      "bytes": 0
   }
   {
      "scope": "user.root",
      "name": "2.png",
      "type": "FILE",
      "parent": null,
      "level": 0,
      "bytes": 0
   }

3.b Get replica for the did using response from 3.a api call 

.. code-block:: javascript

   {{API_BASE_URL}}/replicas/{{scope}}/{{filename}}
   
.. code-block:: javascript

    url = "https://localhost:8443/replicas/user.root/nature7_copy.jpg"

   payload = ""
   headers = {
    'x-rucio-auth-token': 'token',
    'Content-Type': 'application/metalink4+xml'
   }
   response = requests.request("GET", url, headers=headers, data=payload)
   
Response:
.. code-block:: javascript

   {
      "scope": "user.root",
      "name": "nature7_copy.jpg",
      "bytes": 0,
      "md5": null,
      "adler32": "abcdabcd",
      "pfns": {
          "sftp://127.0.0.1:22/sftp/rucio/user/root/ce/71/nature7_copy.jpg": {
              "rse_id": "3afe010ba22448da9a8ef981cc1e9482",
              "rse": "SITE1_DISK",
              "type": "DISK",
              "volatile": false,
              "domain": "wan",
              "priority": 1,
              "client_extract": false
          }
      },
      "rses": {
          "SITE1_DISK": [
              "sftp://127.0.0.1:22/sftp/rucio/user/root/ce/71/nature7_copy.jpg"
          ]
      },
      "states": {
          "SITE1_DISK": "AVAILABLE"
      }
   }

3.c Downalod file using the response of 3.b api call 

.. code-block:: javascript

   {{API_BASE_URL}}/download/{{account}}/{{rse}}/{{scope}}
   
.. code-block:: javascript

   url = "https://localhost:8443/download/root/SITE1_DISK/user.root"

   payload = json.dumps({
    "scope": "user.root",
    "name": "nature7_copy.jpg",
    "bytes": 0,
    "md5": None,
    "adler32": "abcdabcd",
    "pfns": {
      "sftp://127.0.0.1:22/sftp/rucio/user/root/ce/71/nature7_copy.jpg": {
        "rse_id": "3afe010ba22448da9a8ef981cc1e9482",
        "rse": "SITE1_DISK",
        "type": "DISK",
        "volatile": False,
        "domain": "wan",
        "priority": 1,
        "client_extract": False
      }
    },
    "rses": {
      "SITE1_DISK": [
        "sftp://127.0.0.1:22/sftp/rucio/user/root/ce/71/nature7_copy.jpg"
      ]
    },
    "states": {
      "SITE1_DISK": "AVAILABLE"
    }
   })
   headers = {
    'x-rucio-auth-token': Token,
    'Content-Type': 'application/json'
   }

   response = requests.request("GET", url, headers=headers, data=payload)
   open(file_name, 'wb').write(response.content)


