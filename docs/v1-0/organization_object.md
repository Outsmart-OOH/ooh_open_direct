# Organization Object

## Parameters

| Property | Source | Type | Constraints | Add | Update | OOH Supply Side Requirement |
|----------|--------|------|-------------|-----|--------|-----------------------------|
| **Address** | OD | Object | Values provided using ADDRESS object | Optional | Optional | Should support |
| **AdvertiserBrands** | OOHD | Array | Array of Advertiser Brand IDs | Required | Required | Must Support |
| **Contacts** | OD | Object array | No duplicate contact types. Values provided using CONTACT object. | Required | Optional | Must support |
| **Disapproval Reason** | OD | String | Max   255 char | Read-only | Read-only | Must support |
| **Fax** | OD | String | Max 20 char | Optional | Optional | May support |
| **Id** | OD | String | Max 36 char | Read-only | Read-only | Must support |
| **Industry** | OD | Object | Values provided using INDUSTRY reference data | Optional | Optional | May support |
| **OrganizationType** | OOHD | String | Accepted Values are: 'Advertiser', 'Specialist' or 'Agency' | Required | Optional | Must Support |
| **Name** | OD | String | Max 128 char. Cannot be an empty string. Must be unique. | Required | Optional | Must support |
| **Phone** | OD | String | Max 20 char | Optional | Optional | Should support |
| **ProviderData** | OD | CLOB | Max   1000 Char | Optional | Optional | May support |
| **OOHProviderData** | OOHD | Object | See   OOHProviderData object | Optional | Optional | May support |
| **Status** | OD | String | Max 15 char See description for accepted values | Read-only | Read-only | Must support |
| **Url** | OS | String | Max   1,024 char | Optional | Optional | Should support |

## Parameter Details

| Property | Description |
|----------|-------------|
| **Address** | The organization’s corporate headquarters address. |
| **AdvertiserBrands** | Defines the Brand IDs associated with an organisation |
| **Contacts** | A list of one or more contacts within the organization. Available contacts are provided using the CONTACT common object as specified in section 3.2. The list must contain unique contact types (for example, only one billing contact) and at least one billing contact is required. |
| **Disapproval Reason** | The reason why the organization was not registered. Must be specified if Status is Disapproved. |
| **Fax** | The organization’s fax number. |
| **Id** | A system-generated opaque ID that uniquely identifies this resource. |
| **Industry** | An industry label for the organization.    Only required for advertiser organization. |
| **OrganizationType** | The core activity that an organisation undertakes as a business e.g. advertiser, OOH Specialist or Media Agency |
| **Name** | The organization’s display name. |
| **Phone** | The organization’s phone number. |
| **ProviderData** | An opaque CLOB of provider-defined data. Providers may use this field as needed (for example, to store an ID that correlates this object with resources   within their system). Note that any provider that edits this object may override the data in this field. The data should include a marker that you can identify to ensure the data is yours. |
| **OOHProviderData** | The OOHProviderData object is used for Buyers to detail structured information that may be used to identify their order in a Seller's system using their own IDs or references. |
| **Status** | A value that indicates the current state of the approval process. The approval process confirms the organization’s identity. Below lists the possible values.|
| **Url** | A URL to the organization’s website. |

### Status Values

- Pending: The organization is under review.
- Approved: The organization is approved and can create and book  orders.
- Disapproved: The organization’s identity could not be verified. The organization may not create and book orders. The DisapprovalReason property must specify the reason why the organization was not approved.
- Limited: The organization’s identity could not be verified; however, they may create and book orders. This state may affect the products and pricing offered to the organization. The organization may create orders in any state (except where noted); however, they may search for available inventory or reserve and book inventory only in the Approved and Limited states.