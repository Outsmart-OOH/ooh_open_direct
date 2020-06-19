# Schema v1

## Resources

### Objects

| Name   | Schema |
|--------|--------|
| **Account** | resources/accounts/account_object.json |
| **Line**  | resources/lines/line_object.json |
| **Order** | resources/orders/order_object.json |
| **Organization** |  resources/organizations/organization_object.json |
| **Product** | resources/products/product_object.json |
| **Change Request** | |

### URIs

| Object | Type | Schema |
|--------|------|--------|
| **Account** | Request | resources/accounts/account_request.json |
| **Account** | Single Response |  resources/accounts/account_response.json |
| **Account** | Collection Response | resources/accounts/account_collection_response.json |
| **Line** | Request |   |
| **Line** | Single Response | resources/lines/line_response.json |
| **Line** | Collection Response |  resources/lines/line_collection_response.json |
| **Order** | Request |   |
| **Order** | Single Response |  resources/orders/order_response.json |
| **Order** | Collection Response |  resources/orders/order_collection_response.json |
| **Organization** | Request |   |
| **Organization** | Single Response |  resources/organizations/organization_response.json |
| **Organization** | Collection Response |  resources/organizations/organization_collection_response.json |
| **Product** | Request |   |
| **Product** | Single Response | resources/products/product_response.json |
| **Product** | Collection Response |  resources/products/product_collection_response.json |
| **Change Request** | Request |  |
| **Change Request** | Single Response |  |
| **Change Request** | Collection Response |   |

Single Response = The response you would expect when asking for a single object (e.g. GET /accounts/{id})

Collection Response = The response you would expect when asking for a collection of objects (e.g. GET /accounts)

## Common Objects

| Name |  Schema |
|------|---------|
| **Address** | [common/address_object.json](https://raw.githubusercontent.com/Outsmart-OOH/ooh_open_direct/master/schema/v1/common/address_object.json) |
| **AdvertiserBrand** |  common/advertiserBrand_object.json |
| **Contact** |  common/contact_object.json |
| **ProductAvails** |
| **ProductAvailsSearch** |
| **ProductSearch** |
| **OOHProviderData** |  common/oohProviderData_object.json |
| **Size** | common/size_object.json |
| **Segment** |  |
| **Stats** |  |
| **OOHbject** | common/oohject_object.json |
