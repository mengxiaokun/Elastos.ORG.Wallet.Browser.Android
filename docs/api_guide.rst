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

Wallet service testnet: 18.179.207.38:8080
Wallet history testnet: 54.64.220.165:8080
Web wallet and blockchain is
https://wallet-beta.elastos.org/
https://blockchain-beta.elastos.org/

DID service testnet:    18.179.20.67:8080
DID history testnet:    54.64.220.165:8081


Get DID
-----------------------------------------
Get current logined user did.

.. http:get:: http://127.0.0.1:port/api/v1/getDID

   **Parameter**
     none

   **Return**
     The current logined user did.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/getDID
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

Get Balance
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

.. http:get:: http://127.0.0.1:port/api/v1/sendTransfer?amount=(number:`amount`)&toAddress=(string:`public_address`)[&memo=(string:`memo`)][&information=(string:`local info`)]

   **Parameter**
     :[required] amount:    transfer amount
     :[required] toAddress: transfer to
     :[optional] memo:      note which should save on chain.
     :[optional] info:      note which is saved in local.

   **Return**
     The tranaction id.

   **Example request**:

   .. sourcecode:: http

      GET http://127.0.0.1:port/api/v1/sendTransfer?amount=10000&toAddress=EeDUy6TmGSFfVxXVzMpVkxLhqwCqujE1WL&memo=xxx&information=sss

      Host: localhost

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
         ElastosWalletSign.generateRawTransaction()
         http://did-service-testnet/api/1/sendRawTx



