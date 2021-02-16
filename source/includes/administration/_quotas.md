## Quotas

Quotas are used to limit the resource usage on a service connection consumed by an organization. The primary use case for CloudMC is to enforce limited quotas on trial accounts. Quotas can target different resources. For example, number of vCPUs, allocated memory, disk size, network bandwidth, number of public IPs and more.

<!------------------- LIST QUOTAS --------------------->

<!------------------- GET QUOTA ----------------------->

<!------------------- DELETE QUOTA -------------------->

<!------------------- CREATE QUOTA -------------------->

### Create a quota

`POST /quotas`

```shell
curl -X GET "https://cloudmc_endpoint/rest/quotas" \
   -H "MC-Api-Key: your_api_key"
```

> Request body example:

```json
{
  "name": "my-quota-name",
  "serviceConnection": {
    "id": "6abd9b5b-2aad-4732-9177-509d536c5739"
  },
  "ownerOrganization": {
    "id": "976e1d4b-de6f-454b-a189-b12dd1b85112"
  },
  "quotaDetails": [
    {
      "metricIdentifier": "instance.cpu.count",
      "ceiling": 5
    },
    {
      "metricIdentifier": "disk.size.gb",
      "ceiling": 500
    }
  ],
  "defaultForService": true,
  "defaultForTrial": true
}
```

Create a quota owned by an organization for a connection.

Once created, a quota can be applied to any child organization of the quota's owner. This endpoint cannot be used to apply a quota to an organization. See `POST /quotas/apply` instead.

There can only be one default quota and one default trial quota for a connection. Any attempt to create a default quota, when there's already an existing one, will result in the exsting quota losing it's default status.

Required | &nbsp;
-------- | --------
`name`<br/>*string* | Name of the quota. Must be unique across the connection and organization.
`serviceConnection`<br/>*[ServiceConnection](#administration-service-connections)* | Service connection associated to the quota.<br/>*required*: `id`
`quotaDetails`<br/>*Array[QuotaDetails]* | List of `QuotaDetail` making up the quota. A `QuotaDetail` represents a limit on a resource and is directly linked to a `MetricDescriptor`. A `MetricDescriptor` describes a metric offered by the plugin. For more information, consult the SDK documentation.<br/>*required*: `metricIdentifier`, `ceiling`
`quotaDetail.metricIdentifier`<br/>*string* | A unique identifier used to define a `MetricDescriptor`.
`quotaDetail.ceiling`<br/>*number* | The ceiling for this particular quota detail.

Optional | &nbsp;
-------- | --------
`ownerOrganization`<br/>*[Organization](#administration-organization)* | Organization in which the quota will be created. *Defaults to caller's organization*.<br/>*required:* `id`
`defaultForService`<br/>*Boolean* | A flag denoting if this quota is the default quota for this connection. There can only be one default quota per connection/organization.
`defaultForTrial`<br/>*Boolean* | A flat denoting if this quota is the default quota for a trial. There can only be one default trial quota per connection/organization.

The responses' `data` field contains the created [quota](#administration-quota) with its `id`.
