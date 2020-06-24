# URI Schemas

| Resource    | URI                | Verb | Request                      | Response |
|-------------|--------------------|------|------------------------------|------------------------------------|
| **Account** | /accounts          | GET  |                              | accounts_collection_response.json |
|             | /accounts          | POST | accounts_request.json        | accounts_response.json |
|             | /accounts/{id}     | GET  |                              | accounts_response.json |
|             | /accounts?$filter= | GET  |                              | accounts_collection_response.json|
| **Order**   | /accounts/{id}/orders      | GET  |                           | orders_collection_response.json |
|             | /accounts/{id}/orders      | POST | orders_request.json       | orders_response.json |
|             | /accounts/{id}/orders/{id}      | GET  |                           | orders_response.json |
|             | /accounts/{id}/orders?$filter=  | GET  |                           | orders_collection_response.json |
| **Line**    | /accounts/{id}/orders/{id}/lines | GET |                           | lines_collection_response.json |
|             | /accounts/{id}/orders/{id}/lines | POST | lines_request.json       | lines_response.json |
|             | /accounts/{id}/orders/{id}/lines/{id} | GET |                      | lines_response.json |
|             | /accounts/{id}/orders/{id}/lines/{id}?book | PATCH | lines_request.json       | lines_response.json |
|             | /accounts/{id}/orders/{id}/lines/{id}?reserve | PATCH | lines_request.json       | lines_response.json |
|             | /accounts/{id}/orders/{id}/lines/{id}?cancel | PATCH | lines_request.json       | lines_response.json |
|             | /accounts/{id}/orders/{id}/lines/{id}?reset | PATCH | lines_request.json       | lines_response.json |
| **Organization** | /organizations  | GET            | | organizations_collection_response.json |
|                  | /organizations  | POST            | organizations_request.json | organizations_response.json |
|                  | /organizations/{id}  | GET            |  | organizations_response.json |
|                  | /organizations?$filter=   | GET            |  | organizations_collection_response.json |
| **Product** | /products          | GET  |                              | products_collection_response.json |
|             | /products/{id}     | GET  |                              | products_response.json |
|             | /products/search   | POST | products_search_request.json | products_collection_response.json |
|             | /products/avails   | POST | products_avails_request.json | products_avails_collection_response |
| **Advertiser Brands** | /advertiserbrands | GET |   | advertiserbrands_collection_response.json |
|                       | /advertiserbrands/{id} | GET |   | advertiserbrands_response.json |
|                       | /advertiserbrands?$filter= | GET |   | advertiserbrands_collection_response.json |
| **Data Sources** | /datasources | GET |   | datasources_collection_response.json |
|                       | /datasources/{id} | GET |   | datasources_response.json |
|                       | /datasources?$filter= | GET |   | datasources_collection_response.json |
