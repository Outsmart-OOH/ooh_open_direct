# URI Schemas

| Resource | URI | Verb | Request | Response |
|----------|-----|------|---------|----------|
| **Account** | /accounts | GET |  | accounts_collection_response.json |
|             | /accounts | POST | accounts_request.json | accounts_response.json |
|             | /accounts/{id} | GET |  | accounts_response.json | |
|             | /accounts?$filter= | GET |  | accounts_collection_response.json|
| **Product** | /products | GET |  | products_collection_response.json |
|             | /products/{id} | GET |  | products_response.json | |
|             | /products/search | POST | products_search_request.json | |
|             | /products/avails | POST | products_avails_request.json | |
