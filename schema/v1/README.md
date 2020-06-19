# Schema v0

## Current State of Development

| State | Description |
|-------|-------------|
| **None** | Not created |
| **Dev**  | In Development, not yet finished |
| **Dev Done** | Development done |
| **Tested** | Tested against spec and examples |
| **Complete** | Done, Tested and Complete |

## Resources

### Objects

| Name   | State | Schema |
|---|---|---|
| **Account** | Dev | resources/accounts/account_object.json |
| **Line** | Dev | resources/lines/line_object.json |
| **Order** | Dev Done | resources/orders/order_object.json |
| **Organization** | Dev Done | resources/organizations/organization_object.json |
| **Product** | Dev Done | resources/products/product_object.json |
| **Change Request** | None | |

### URIs

| Object | Type | State | Schema |
|--------|---|---|---|
| **Account** | Request | Dev Done | resources/accounts/account_request.json |
| **Account** | Single Response | Dev Done | resources/accounts/account_response.json |
| **Account** | Collection Response | Dev Done | resources/accounts/account_collection_response.json |
| **Line** | Request | None |  |
| **Line** | Single Response | Dev Done | resources/lines/line_response.json |
| **Line** | Collection Response | Dev Done | resources/lines/line_collection_response.json |
| **Order** | Request | None |  |
| **Order** | Single Response | Dev Done | resources/orders/order_response.json |
| **Order** | Collection Response | Dev Done | resources/orders/order_collection_response.json |
| **Organization** | Request | None |  |
| **Organization** | Single Response | Dev Done | resources/organizations/organization_response.json |
| **Organization** | Collection Response | Dev Done | resources/organizations/organization_collection_response.json |
| **Product** | Request | None |  |
| **Product** | Single Response | Dev Done | resources/products/product_response.json |
| **Product** | Collection Response | Dev Done | resources/products/product_collection_response.json |
| **Change Request** | Request | None |  |
| **Change Request** | Single Response | None |  |
| **Change Request** | Collection Response | None |  |

Single Response = The response you would expect when asking for a single object (e.g. GET /accounts/{id})

Collection Response = The response you would expect when asking for a collection of objects (e.g. GET /accounts)

## Common Objects

| Name | State | Schema |
|------|-------|------|
| **Address** | Dev Done | [common/address_object.json](https://raw.githubusercontent.com/Outsmart-OOH/ooh_open_direct/master/schema/v1/common/address_object.json) |
| **AdvertiserBrand** | Dev Done | common/advertiserBrand_object.json |
| **Contact** | Dev Done | common/contact_object.json |
| **ProductAvails** |
| **ProductAvailsSearch** |
| **ProductSearch** |
| **OOHProviderData** | Dev | common/oohProviderData_object.json |
| **Size** | Dev Done | common/size_object.json |
| **Segment** | None | |
| **Stats** | None | |
| **OOHbject** | Dev Done | common/oohject_object.json |
