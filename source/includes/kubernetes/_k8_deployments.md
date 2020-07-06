## Deployments

<!-------------------- LIST DEPLOYMENTS -------------------->

#### List deployments

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/deployments"
```

> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "id": "apm-server-1585600296-apm-server/monitoring",
      "deploymentStatus": "Available",
      "readyRatio": "1/1",
      "metadata": {},
      "spec": {},
      "status": {}
    }
  ],  
  "metadata": {
    "recordCount": 9
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/deployments</code>

Retrieve a list of all deployments in a given [environment](#administration-environments).

| Attributes                                 | &nbsp;                                                          |
| ------------------------------------------ | --------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the deployment                                        |
| `metadata` <br/>_object_                   | The metadata of the deployment                                  |
| `metadata.name` <br/>_string_              | The name of the deployment                                      |
| `metadata.namespace` <br/>_string_         | The namespace in which the deployment is created                |
| `metadata.uid` <br/>_object_               | The UUID of the deployment                                      |
| `images` <br/>_object_                     | The container images within a deployment                        |
| `spec`<br/>_object_                        | The specification used to create and run the deployment         |
| `status`<br/>_object_                      | The status information of the deployment                        |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET A DEPLOYMENT -------------------->

#### Get a deployment

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/deployments/test-aerospike/auth"
```

> The above command returns a JSON structured like this:

```json
{
    "data": {
      "id": "apm-server-1585600296-apm-server/monitoring",
      "deploymentStatus": "Available",
      "readyRatio": "1/1",
      "metadata": {},
      "spec": {},
      "status": {}
    }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/deployments/:id</code>

Retrieve a deployment and all its info in a given [environment](#administration-environments).

| Attributes                                 | &nbsp;                                                          |
| ------------------------------------------ | --------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the deployment                                        |
| `metadata` <br/>_object_                   | The metadata of the deployment                                  |
| `images` <br/>_object_                     | The container images within a deployment                        |
| `spec`<br/>_object_                        | The specification used to create and run the deployment         |
| `status`<br/>_object_                      | The status information of the deployment                        |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).