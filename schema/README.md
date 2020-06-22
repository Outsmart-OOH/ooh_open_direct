# OpenDirect OOH Schemas

## v1 Schema

Published version of Schema to match v1 of OpenDirect (OOH) 1.5.1 v1

| Resource | URI | Verb | Request | Response |
|-------------|--------------------|------|------------------------------|------------------------------------|
| **Account** | /accounts          | GET  |                              | accounts_collection_response.json |
|             | /accounts          | POST | accounts_request.json        | accounts_response.json |
|             | /accounts/{id}     | GET  |                              | accounts_response.json |
|             | /accounts?$filter= | GET  |                              | accounts_collection_response.json|
| **Product** | /products          | GET  |                              | products_collection_response.json |
|             | /products/{id}     | GET  |                              | products_response.json |
|             | /products/search   | POST | products_search_request.json | products_collection_response.json |
|             | /products/avails   | POST | products_avails_request.json | products_avails_collection_response |

## v0 Schema

Development Schema while building the spec
