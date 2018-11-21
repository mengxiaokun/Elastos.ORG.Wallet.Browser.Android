Getting started with the nodela API
########################################

.. toctree::
  :maxdepth: 3

Introduction
=============
Nodela has a Restful API with URL endpoints corresponding to actions that users can perform with their channels. The endpoints accept and return JSON encoded objects. The API URL path always contains the API version in order to differentiate queries to different API versions. All queries start with: ``/api/<version>/`` where ``<version>`` is an integer representing the current API version.

.. api:

API
=================================
using the following api ,we can easyly get a glimps of what is going on in the blockchain.

Web wallet and blockchain:

.. note::
   https://wallet-beta.elastos.org/
   https://blockchain-beta.elastos.org/

Testnet address

.. note::
   wallet-service-testnet: 18.179.207.38:8080
   wallet-history-testnet: 54.64.220.165:8080
   did-service-testnet:    18.179.20.67:8080
   did-history-testnet:    54.64.220.165:8081


Get Did
-----------------------------------------
Get current logined user did.

.. http:get:: http://127.0.0.1:port/api/v1/getDid

   **Parameter**
     none

   **Return**
     The current logined user did.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getDid
      Host: localhost

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result":"iQZCB3NfXRhba6FqpE2WSs6UnAHgFyCX5B"
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: ElastosWalletDID.getDid()


Get candy address
-----------------------------------------
Get current logined user address.

.. http:get:: http://127.0.0.1:port/api/v1/getAddress

   **Parameter**
     none

   **Return**
     The current logined user address.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getAddress
      Host: localhost

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result":"EJonBz8U1gYnANjSafRF9EAJW9KTwRKd6x"
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: ElastosWallet.getAddress()


Get balance
-----------------------------------------
Get current logined user balance.

.. http:get:: http://127.0.0.1:port/api/v1/getBalance

   **Parameter**
     none

   **Return**
     The current logined user balance. units is sela, 1 ela = 100000000 sela.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getBalance
      Host: localhost

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result":"1000000"
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: http://did-service-testnet/api/1/balance/(string:`public_address`)


Send transfer
-----------------------------------------
Send a transfer to id-chain.

.. http:get:: http://127.0.0.1:port/api/v1/sendTransfer

   **Parameter**
     None

   **Return**
     The tranaction id.

   **Example request**:

   .. sourcecode:: http

      POST http://127.0.0.1:port/api/v1/sendTransfer
      Host: localhost
      Content-Type: application/json
      {
        "amount": 10000,
        "toAddress": "EeDUy6TmGSFfVxXVzMpVkxLhqwCqujE1WL",
        "memo": "xxx",
        "info": "sss"
      }

      #amount: [required] transfer amount. units is sela, 1 ela = 100000000 sela.
      #toAddress: [required] transfer to
      #memo: [optional] note which should save on id-chain.
      #info: [optional] note which is saved in local.

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result":"1f4432635bcf8c347f2bc20b7906c8c6c195f51beb3426e5f8d6a9e4cc073cf3"
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: http://did-service-testnet/api/1/createTx
   :Ref: ElastosWalletSign.generateRawTransaction()
   :Ref: http://did-service-testnet/api/1/sendRawTx


Get transaction by transaction id
-----------------------------------------
Check out a transaction.

.. http:get:: http://127.0.0.1:port/api/v1/getTxById?txId=(string:`txid`)

   **Parameter**
     :txId: [required] transaction id.

   **Return**
     The tranaction data.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getTxById?txId=cd21b8729ca6173862034fb5515d395c25e5c7779330aa3634d7128435ddd4f4
      Host: localhost

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
        "status":200,
        "result":{
          "Txid": "cd21b8729ca6173862034fb5515d395c25e5c7779330aa3634d7128435ddd4f4",
          "Type": "sending",
          "Value": "100",
          "CreateTime": "1541755973",
          "Height": 157576,
          "Fee": "1",
          "Inputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"],
          "Outputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT",
                      "EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"]
        }
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: http://did-service-testnet/api/1/tx/(string:`txid`)


Get all transactions.
-----------------------------------------
Check out all transactions of logined user.

.. http:get:: http://127.0.0.1:port/api/v1/getAllTxs[?][pageNum=(number:`page number`)]
                                                    [&][pageSize=(number:`page size`)]

   **Parameter**
     :pageNum:  [optional] page number, if not set, use 0.
     :pageSize: [optional] page size, if not set, use -1, and return all transactions.

   **Return**
     All the tranaction data.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getAllTxs?pageNum=1&pageSize=3
      Host: localhost

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
        "status": 200
        "result": {
          "History": [{
            "Txid": "cd21b8729ca6173862034fb5515d395c25e5c7779330aa3634d7128435ddd4f4",
            "Type": "sending",
            "Value": "100",
            "CreateTime": "1541755973",
            "Height": 157576,
            "Fee": "1",
            "Inputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"],
            "Outputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT", "EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"]
          }, {
            "Txid": "1e368ad6af41fb626d35f6e2dac238b6b64bfadcf3d3f297919f81029e0027ff",
            "Type": "spend",
            "Value": "101000",
            "CreateTime": "1542089418",
            "Height": 160171,
            "Fee": "100",
            "Inputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"],
            "Outputs": ["EMHc9JSpxKWbTMf8gQDcWm7Tz1C5nQNA8Z", "EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT"]
          }, {
            "Txid": "17649d6b4a98b1834f51b4a319568a89669a6e4ae89d33a8188c8743bb51b62d",
            "Type": "income",
            "Value": "8000000",
            "CreateTime": "1542263232",
            "Height": 161512,
            "Fee": "1",
            "Inputs": ["EaVuwkuk9gMcCRX28FRqrmQZh3KUuXJnzL"],
            "Outputs": ["EbAATdrW7gaomFY3SAy81rokqwqKA3EXbT", "EaVuwkuk9gMcCRX28FRqrmQZh3KUuXJnzL"]
          }],
          "TotalNum": 8
        },
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: http://did-history-testnet/history/(string:`public address`)?pageNum=(number:`page num`)&pageSize=(number:`page size`)


Set DID information
-----------------------------------------
Get did information.

.. http:post:: http://127.0.0.1:port/api/v1/setDidInfo

   **Parameter**
     none

   **Return**
     The tranaction id.

   **Example request**:

   .. sourcecode:: http

      POST http://127.0.0.1:port/api/v1/setDidInfo
      Host: localhost
      Content-Type: application/json
      {
        "key1": "value1",
        "key2": "value2",
        "key3": "value3"
      }

      #key:   [required] Name
      #value: [required] Value of key,
                         If the value is null, key is mark as ignored.
                         If the value is "", key is mark as removed.

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result":"1f4432635bcf8c347f2bc20b7906c8c6c195f51beb3426e5f8d6a9e4cc073cf3"
      }

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: UNIMPLEMENTED. Temporarily set to local.

Get DID information
-----------------------------------------
Get did information.

.. http:post:: http://127.0.0.1:port/api/v1/getDidInfo

   **Parameter**
     none

   **Return**
     The tranaction id.

   **Example request**:

   .. sourcecode:: http

      POST http://127.0.0.1:port/api/v1/getDidInfo
      Host: localhost
      Content-Type: application/json
      [
        "key1",
        "key2",
        "key3"
      ]

      #key:   [required] Name

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json
      {
          "status":200,
          "result": {
            "key1": "value1",
            "key2": null,
            "key3": ""
          }
      }

      #value: [required] Value of key,
                         If the value is null, key is mark as ignored.
                         If the value is "", key is mark as removed.

   :statuscode 200:   no error
   :statuscode 400:   bad request
   :statuscode 500:   internal error
   :statuscode 10001: process error

   :Ref: UNIMPLEMENTED. Temporarily get from local.

