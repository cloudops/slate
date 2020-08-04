#### StatefulSets

<!-------------------- LIST STATEFULSETS -------------------->

##### List statefulsets

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/statefulsets?cluster_id=a_cluster_id"
```

> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "id": "test-aerospike/auth",
      "images": ["aerospike/aerospike-server:4.5.0.5"],
      "metadata": {},
      "spec": {},
      "status": {}
    }
  ],
  "metadata": {
    "recordCount": 4
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/statefulsets?cluster_id=:cluster_id</code>

Retrieve a list of all statefulsets in a given [environment](#administration-environments).

| Required                   | &nbsp;                                                   |
| -------------------------- | -------------------------------------------------------- |
| `cluster_id` <br/>_string_ | The id of the cluster in which to list the statefulsets. |

| Attributes               | &nbsp;                                                    |
| ------------------------ | --------------------------------------------------------- |
| `id` <br/>_string_       | The id of the statefulset.                                |
| `metadata` <br/>_object_ | The metadata of the statefulset.                          |
| `spec`<br/>_object_      | The specification used to create and run the statefulset. |
| `status`<br/>_object_    | The status information of the statefulset.                |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET A STATEFULSET -------------------->

##### Get a statefulset

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/statefulsets/test-aerospike/auth?cluster_id=a_cluster_id"
```

> The above command returns a JSON structured like this:

```json
{
  "data": {
    "id": "test-aerospike/auth",
    "replicaRatio": "1 / 1",
    "images": ["aerospike/aerospike-server:4.5.0.5"],
    "apiVersion": "apps/v1",
    "kind": "StatefulSet",
    "metadata": {},
    "spec": {},
    "status": {}
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/statefulsets/:id?cluster_id=:cluster_id</code>

Retrieve a statefulset and all its info in a given [environment](#administration-environments).

| Required                   | &nbsp;                                                 |
| -------------------------- | ------------------------------------------------------ |
| `cluster_id` <br/>_string_ | The id of the cluster in which to get the statefulset. |
| `id` <br/>_string_         | The id of the statefulset.                             |

| Attributes               | &nbsp;                                                    |
| ------------------------ | --------------------------------------------------------- |
| `metadata` <br/>_object_ | The metadata of the statefulset.                          |
| `spec`<br/>_object_      | The specification used to create and run the statefulset. |
| `status`<br/>_object_    | The status information of the statefulset.                |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- CREATE A STATEFULSET -------------------->

##### Create a statefulset

```shell
curl -X POST \
  -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/statefulsets?cluster_id=a_cluster_id"
  Content-Type: application/json
  {
  "apiVersion": "apps/v1",
  "kind":"StatefulSet",
  "metadata": {
    "name": "stateful-set-name",
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
            "image": "k8s.gcr.io/nginx-slim:0.8"
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

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/statefulsets?cluster_id=:cluster_id</code>

Create a statefulset in a given [environment](#administration-environments).

| Required Attributes           | &nbsp;                                                                      |
| ----------------------------- | --------------------------------------------------------------------------- |
| `cluster_id` <br/>_string_    | The id of the cluster in which to delete the statefulset.                   |
| `apiVersion` <br/> _string_   | The api version (versioned schema) of the statefulset.                      |
| `metadata` <br/>_object_      | The metadata of the statefulset.                                            |
| `metadata.name` <br/>_string_ | The name of the statefulset.                                                |
| `spec`<br/>_object_           | The specification used to create and run the statefulset.                   |
| `spec.selector`<br/>_object_  | The label query over the statefulset's resources.                           |
| `spec.template`<br/>_object_  | The data a statefulset's pod should have when created.                      |
| `spec.spec`<br/>_object_      | The specification used to create and run the pod(s) within the statefulset. |

| Optional Attributes                      | &nbsp;                                                                  |
| ---------------------------------------- | ----------------------------------------------------------------------- |
| `kind`<br/>_string_                      | The string value representing the REST resource this object represents. |
| `metadata.namespace` <br/>_string_       | The namespace in which the statefulset is created.                      |
| `spec.selector.matchLabels`<br/>_object_ | The key value pairs retrieved by a label query from a statefulset.      |

Return value:

| Attributes                 | &nbsp;                                               |
| -------------------------- | ---------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the create statefulset task. |
| `taskStatus` <br/>_string_ | The status of the operation.                         |

<!-------------------- DELETE A STATEFULSET -------------------->

##### Delete a statefulset

```shell
curl -X DELETE \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/statefulsets/my-aerospike/default"
```

> The above command returns a JSON structured like this:

```json
{
  "taskId": "1542bd45-4732-419b-87b6-4ea6ec695c2b",
  "taskStatus": "PENDING"
}
```

<code>DELETE /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/statefulsets/:id?cluster_id=:cluster_id</code>

Delete a statefulset from a given [environment](#administration-environments).

| Required                   | &nbsp;                                                    |
| -------------------------- | --------------------------------------------------------- |
| `cluster_id` <br/>_string_ | The id of the cluster in which to delete the statefulset. |
| `id` <br/>_string_         | The id of the statefulset.                                |

Return value:

| Attributes                 | &nbsp;                                               |
| -------------------------- | ---------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the delete statefulset task. |
| `taskStatus` <br/>_string_ | The status of the operation.                         |
