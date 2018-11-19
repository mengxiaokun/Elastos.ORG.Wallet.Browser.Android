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

Get DID
-----------------------------------------
Get current logined user did.

.. http:get:: http://127.0.0.1:port/api/v1/getDID

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
Get current logined user balance, return units is sela, 1 ela = 100000000 sela.

.. http:get:: http://127.0.0.1:port/api/v1/getBalance

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

   :Ref: http://18.179.20.67:8080/api/1/balance/(string:`public_address`)


