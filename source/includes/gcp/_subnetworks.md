### Subnetworks
Create and manage your subnetworks. Subnetworks belongs to a network.

<!-------------------- LIST INSTANCES -------------------->

#### List subnetworks

```shell
curl -X GET \
  -H "mc-api-key: MSzI0RPkdvMgU9Y68oGRsw==" \
  "https://cloudmc_endpoint/v1/services/gcp/test-area/subnetworks"
```
> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "creationTimestamp": "2020-05-28T07:20:17.315-07:00",
      "fingerprint": "6S1Xfr1s97Y=",
      "gatewayAddress": "10.128.0.1",
      "ipCidrRange": "10.128.0.0/20",
      "kind": "compute#subnetwork",
      "network": "https://www.googleapis.com/compute/v1/projects/cmc-ankhang-gcp-env-ggb/global/networks/default",
      "privateIpGoogleAccess": false,
      "region": "https://www.googleapis.com/compute/v1/projects/cmc-ankhang-gcp-env-ggb/regions/us-central1",
      "selfLink": "https://www.googleapis.com/compute/v1/projects/cmc-ankhang-gcp-env-ggb/regions/us-central1/subnetworks/default",
      "shortNetwork": "default",
      "id": "5575250766523954766",
      "name": "default",
      "shortRegion": "us-central1"
    }],
  "metadata": {
    "recordCount": 1
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/subnetworks</code>

Retrieve a list of all networks in a given [environment](#administration-environments).

#### Filters:

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/subnetworks?network=<a href="#VPC-network-selflink">:VPC-network-selflink</a></code>

Retrieve a list of all networks in a given [environment](#administration-environments) and [VPC-network].

Attributes | &nbsp;
------- | -----------
`creationTimestamp`<br/>*string* | Creation timestamp in RFC3339 text format
`fingerprint`<br/>*string* | A base64-encoded string. A hash of the label's contents and used for optimistic locking
`gatewayAddress`<br/>*string* | Second address in the primary IP range for the subnet
`ipCidrRange`<br/>*string* | Primary IP address range for the following resources: VM instances, internal load balancers, and internal protocol forwarding
`kind`<br/>*string* | Type of the resource
`network`<br/>*string* | Server-defined URL for the VPC network that contains the subnet
`privateIpGoogleAccess`<br/>*string* | Whether the Private Google Access is configured
`region`<br/>*Array[Disk]* | Server-defined URL for the region name
`selfLink`<br/>*string* | Server-defined URL for this resource
`shortNetwork`<br/>*string* | Display name of the VPC network that contains the subnet
`id`<br/>*UUID* | The id of the instance
`name`<br/>*string* | The display name of the subnetwork.
`shortRegion`<br/>*string* | A short version of the region name

<!-------------------- CREATE A SUBNETWORK -------------------->

#### Create a subnet

```shell
curl -X POST \
   -H "Content-Type: application/json" \
   -H "MC-Api-Key: your_api_key" \
   -d "request_body" \
   "https://cloudmc_endpoint/v1/services/gcp/test-area/subnetworks"
}'
```
> Request body example:

```json
{
  "name": "my-subnet",
  "shortRegion": "northamerica-northeast1",
  "ipCidrRange": "10.0.0.0/9",
  "network": "https://www.googleapis.com/compute/v1/projects/my-project/global/networks/my-network"
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/subnetworks</code>

Create a new subnetwork

Required | &nbsp;
------- | -----------
`name`<br/>*string* | The display name of the instance
`shortRegion`<br/>*string* | A short version of the region name
`network`<br/>*string* | The selflink of the network
`ipCidrRange`<br/>*string* | The CIDR IP range of the subnetwork

Optional | &nbsp;
------- | -----------
`description`<br/>*string* | Description of the subnet