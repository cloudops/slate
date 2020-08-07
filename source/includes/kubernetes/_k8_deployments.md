### Deployments

<!-------------------- LIST DEPLOYMENTS -------------------->

###### List deployments

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
| `id` <br/>_string_                         | The id of the deployment.                                       |
| `metadata` <br/>_object_                   | The metadata of the deployment.                                 |
| `metadata.name` <br/>_string_              | The name of the deployment.                                     |
| `metadata.namespace` <br/>_string_         | The namespace in which the deployment is created.               |
| `metadata.uid` <br/>_object_               | The UUID of the deployment.                                     |
| `images` <br/>_object_                     | The container images within a deployment.                       |
| `spec`<br/>_object_                        | The specification used to create and run the deployment.        |
| `status`<br/>_object_                      | The status information of the deployment.                       |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET A DEPLOYMENT -------------------->

###### Get a deployment

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

| Attributes                                 | &nbsp;                                                            |
| ------------------------------------------ | ----------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the deployment.                                         |
| `deplomentStatus`<br/>_object_             | The status information of the deployment.                         |
| `readyRatio` <br/>_object_                 | The ready replicas to total replicas ratio of this deployment set.|
| `metadata` <br/>_object_                   | The metadata of the deployment.                                   |
| `spec`<br/>_object_                        | The specification used to create and run the deployment.          |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- CREATE DEPLOYMENT -------------------->

#### Create a deployment

```shell
curl -X POST \
  -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/deployments"
  Content-Type: application/json
  {
  "apiVersion": "apps/v1",
  "kind": "Deployment",
  "metadata": {
    "name": "api-test-deployment-name",
    "namespace": "default"
  },
  "spec": {
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx"
          }
        ]
      }
    }
  }
}
```

> The above command returns a JSON structured like this:

```json
{
  "taskId": "1542bd45-4732-419b-87b6-4ea6ec695c2b",
  "taskStatus": "PENDING"
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/deployments</code>

Create a deployment in a given [environment](#administration-environments).

| Required Attributes                        | &nbsp;                                                                     |
| ------------------------------------------ | -------------------------------------------------------------------------- |
| `apiVersion` <br/> _string_                | The api version (versioned schema) of the deployment.                      |
| `metadata` <br/>_object_                   | The metadata of the deployment.                                            |
| `metadata.name` <br/>_string_              | The name of the deployment.                                                |
| `spec`<br/>_object_                        | The specification used to create and run the deployment.                   |
| `spec.selector`<br/>_object_               | The label query over the deployment's set of resources.                    |
| `spec.template`<br/>_object_               | The data a deployment's pod should have when created.                      |
| `spec.spec`<br/>*object*                   | The specification used to create and run the pod(s) within the deployment. |

| Optional Attributes                        | &nbsp;                                                                     |
| ------------------------------------------ | -------------------------------------------------------------------------- |
| `kind`<br/>_string_                        | The string value of the REST resource that this object represents.         |
| `metadata.namespace` <br/>_string_         | The namespace in which the deployment is created.                          |
| `spec.selector.matchLabels`<br/>_object_   | The key value pairs retrieved by a label query from a deployment.          |

Return value:

| Attributes                 | &nbsp;                                              |
| -------------------------- | --------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the create deployment task. |
| `taskStatus` <br/>_string_ | The status of the operation.                        |

<!-------------------- DELETE DEPLOYMENT -------------------->

#### Delete a deployment

```shell
curl -X DELETE \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/deployments/dex/auth"
```

> The above command returns a JSON structured like this:

```json
{
  "taskId": "1542bd45-4732-419b-87b6-4ea6ec695c2b",
  "taskStatus": "PENDING"
}
```

<code>DELETE /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/deployments/:id</code>

Delete a deployment from a given [environment](#administration-environments).

| Attributes                 | &nbsp;                                              |
| -------------------------- | --------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the delete deployment task. |
| `taskStatus` <br/>_string_ | The status of the operation.                        |