## Organizations
Organizations are the largest logical grouping of users, environments and resources available in Cox Edge. Each organization is isolated from other organizations. It is protected by its own customizable system [roles](#administration-roles). Additionally, provisioned resource usage is metered at the organization level facilitating cost tracking.


<!-------------------- LIST ORGANIZATIONS -------------------->
### List organizations

`GET /organizations`

Retrieves a list of organizations visible to the caller. In most cases, only the caller's organization will be returned. However if the caller's organization has sub-organizations, and the caller has the `Access other levels` permission, the sub-organizations will be returned as well.

```shell
# Retrieve visible organizations
curl "https://portal.coxedge.com/api/v1/organizations" \
   -H "MC-Api-Key: your_api_key"
```    
> The above command returns a JSON structured like this:

```json
{
   "data": [
      {
         "id": "03bc22bd-adc4-46b8-988d-afddc24c0cb5",
         "name": "Umbrella Corporation",
         "entryPoint": "umbrella",
         "billableStartDate": "2017-08-15T12:00:00.000Z",
         "billingDay": 5,
         "isBillable": true,
         "billingMode": "CREDIT_CARD",
         "isReseller": false,
         "tags": ["a-tag"],
         "parent": {
            "id": "8e3393ce-ee63-4f32-9e0f-7b0200fa655a",
            "name": "Capcom"
         },
         "environments": [
            {
               "id": "9df14056-51e2-4000-ab14-beeaa488500d"
            }
         ],
         "roles": [
            {
               "id": "cdaaa9d0-304e-4063-b1ab-de31905bdab8"
            }
         ],
         "serviceConnections":[
            {
               "id":"11607a49-9691-40fe-8022-2e148bc0d720",
            }
         ],
         "users": [
            {
               "id":"0c3ffcce-a98d-4159-b6fc-04edd34e89b7",
               "userName":"wbirkin"
            }
         ]
      }
   ]
}
```

Attributes | &nbsp;
---- | -----------
`id`<br/>*UUID* | The id of the organization.
`name`<br/>*string* | The name of the organization.
`entryPoint`<br/>*string* | The entry point of the organization is the subdomain of the organization in the Cox Edge URL : `[entryPoint].Cox Edge`.
`billableStartDate`<br/>*string* | The billable start date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) of the organization.
`billingDay`<br/>*int* | The billing day of the organization. Default value is 1.
`isBillable`<br/>*boolean* | If the organization is billable this values is true, false otherwise.
`billingMode`<br/>*enum* | The billing mode of the organization. It could be either "MANUAL" or "CREDIT_CARD". Default value is "MANUAL".
`tags`<br/>*Array[string]* | Tags associated to the organization.
`parent`<br/>*[Organization](#administration-organizations)* | If the organization is a sub-organization, it will have its `parent` organization. *includes*:`id`,`name`.
`environments`<br/>*Array[[Environment](#administration-environments)]* | The environments belonging to the organization.<br/>*includes*: `id`
`roles`<br/>*Array[[Role](#administration-roles)]* | The system and environments roles belonging to the organization.<br/>*includes*: `id`
`serviceConnections`<br/>*Array[[ServiceConnection](#administration-service-connections)]* | The services for which the organization is allowed to provision resources.<br/>*includes*: `id`,`serviceCode`
`resourceCommitments`</br>*Array[[ResourceCommitment](#administration-retrieve-a-resource-commitment)]* | The resource commitments applied on the organization.
`users`<br/>*Array[[User](#administration-users)]* | The users of the organization.<br/>*includes*: `id`
`notes`<br/>*string* | Organization notes.
`isDbAuthentication`<br/>*boolean* | Whether or not the organization supports database authentication.
`isLdapAuthentication`<br/>*boolean* | Whether or not LDAP authentication is enabled on this organization.
`isTrial`<br/>*boolean* | Whether or not this is a trial organization.
`isReseller`<br/>*boolean* | Whether or not this organization is a reseller or not.
`customDomain`<br/>*[VerifiedDomain](#administration-get-verified-domains)* | The custom domain for the organization.

<!-------------------- FIND ORGANIZATION -------------------->
### Retrieve an organization

`GET /organizations/:id`

Retrieve an organization's details.

```shell
# Retrieve an organization
curl "https://portal.coxedge.com/api/v1/organizations/03bc22bd-adc4-46b8-988d-afddc24c0cb5" \
   -H "MC-Api-Key: your_api_key"
```
> The above command returns a JSON structured like this:

```json
{
   "data": {
      "id": "03bc22bd-adc4-46b8-988d-afddc24c0cb5",
      "name": "Nintendo US",
      "entryPoint": "nintendo-us",
      "billableStartDate": "2017-08-15T12:00:00.000Z",
      "billingDay": 5,
      "isBillable": true,
      "billingMode": "CREDIT_CARD",
      "isReseller": false,
      "tags": ["a-tag"],
      "parent": {
         "id": "8e3393ce-ee63-4f32-9e0f-7b0200fa655a",
         "name": "Nintendo"
      },
      "environments": [
         {
           "id": "9df14056-51e2-4000-ab14-beeaa488500d"
         }
      ],
      "roles": [
         {
           "id": "cdaaa9d0-304e-4063-b1ab-de31905bdab8"
         }
      ],
      "serviceConnections": [
         {
            "id":"11607a49-9691-40fe-8022-2e148bc0d720",
            "serviceCode":"edge"
         }
      ],
      "users": [
         {
            "id":"0c3ffcce-a98d-4159-b6fc-04edd34e89b7",
            "userName":"reggie"
         }
      ]
  }
}
```

Attributes | &nbsp;
---- | -----------
`id`<br/>*UUID* | The id of the organization.
`name`<br/>*string* | The name of the organization.
`entryPoint`<br/>*string* | The entry point of the organization is the subdomain of the organization in the Cox Edge URL :<br/>`[entryPoint].Cox Edge`.
`billableStartDate`<br/>*string* | The billable start date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) of the organization.
`billingDay`<br/>*int* | The billing day of the organization. Default value is 1.
`isBillable`<br/>*boolean* | If the organization is billable this values is true, false otherwise.
`billingMode`<br/>*enum* | The billing mode of the organization. It could be either "MANUAL" or "CREDIT_CARD". Default value is "MANUAL".
`tags`<br/>*Array[string]* | Tags associated to the organization.
`parent`<br/>*[Organization](#administration-organizations)* | If the organization is a sub-organization, it will have its `parent` organization. *includes*:`id`,`name`.
`environments`<br/>*Array[[Environment](#administration-environments)]* | The environments belonging to the organization.<br/>*includes*: `id`
`roles`<br/>*Array[[Role](#administration-roles)]* | The system and environments roles belonging to the organization.<br/>*includes*: `id`
`serviceConnections`<br/>*Array[[ServiceConnection](#administration-service-connections)]* | The services for which the organization is allowed to provision resources.<br/>*includes*: `id`,`serviceCode`
`resourceCommitments`</br>*Array[[ResourceCommitment](#administration-retrieve-a-resource-commitment)]* | The resource commitments applied on the organization.
`users`<br/>*Array[[User](#administration-users)]* | The users of the organization.<br/>*includes*: `id`
`notes`<br/>*string* | Organization notes.
`isDbAuthentication`<br/>*boolean* | Whether or not the organization supports database authentication.
`isLdapAuthentication`<br/>*boolean* | Whether or not LDAP authentication is enabled on this organization.
`isTrial`<br/>*boolean* | Whether or not this is a trial organization.
`isReseller`<br/>*boolean* | Whether or not this organization is a reseller or not.
`customDomain`<br/>*[VerifiedDomain](#administration-get-verified-domains)* | The custom domain for the organization.

<!-------------------- GET BILLING -------------------->
### Get billing information
`GET /organizations/:organization_id/billing_info`

Retrieve the billing information for an organization.

```shell
# Retrieve the organization's billing information
curl "https://portal.coxedge.com/api/v1/organizations/87895f43-51c1-43cc-b987-7e301bf5b86a/billing_info" \
   -H "MC-Api-Key: your_api_key"
```
> The above command returns a JSON structured like this:

```json
{
  "data": {
    "id": "23910576-d29f-4c14-b663-31d728ff49a5",
    "organization": {
      "id": "23910576-d29f-4c14-b663-31d728ff49a5"
    },
    "billingProvider": {
      "id": "f26e66a4-755c-4867-b565-ad68aa515237"
    },
    "cardType": "Mastercard",
    "cardMaskedNumber": "************1234",
    "cardName": "John Doe",
    "cardExp": "0124",
    "billingAddressLineOne": "555 SomeStree",
    "billingAddressLineTwo": "App #2",
    "billingAddressCity": "SomeCity",
    "billingAddressProvince": "NY",
    "billingAddressPostalCode": "555555",
    "billingAddressCountry": "US"
  }
}
```
Attributes | &nbsp;
---- | -----------
`id`<br/>*UUID* | The id of the billing information.
`organization`<br/>*[Organization](#administration-organizations)* | The organization to which belongs the billing information.
`billingProvider`<br/>*[BillingProvier](#administration-billing-providers)* | The billing provider associated to the credit card.
`cardType`<br/>*string* | The credit card type.
`cardMaskedNumber`<br/>*string* | The credit card masked number.
`cardName`<br/>*string* | The name on the credit card 
`cardExp`<br/>*string* | The credit card expiration ('mmyy' format)
`billingAddressLineOne`<br/>*string* | The address line 1 of the billing address.
`billingAddressLineTwo`<br/>*string* | The address line 2 of the billing address.
`billingAddressCity`<br/>*string* | The city of the billing address.
`billingAddressProvince`<br/>*string* | The province or state code (2 letters) of the billing address.
`billingAddressPostalCode`<br/>*string* | The postal/zip code of the billing address.
`billingAddressCountry`<br/>*string* | The country code (ISO 2 or 3 letter code) of the billing address
