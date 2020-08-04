### DaemonSets

<!-------------------- LIST DAEMONSETS -------------------->

#### List daemonsets

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/daemonsets"
```

> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "id": "canal/kube-system",
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

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/daemonsets</code>

Retrieve a list of all daemonsets in a given [environment](#administration-environments).

| Attributes               | &nbsp;                                                  |
| ------------------------ | ------------------------------------------------------- |
| `id` <br/>_string_       | The id of the daemonset.                                |
| `metadata` <br/>_object_ | The metadata of the daemonset.                          |
| `spec`<br/>_object_      | The specification used to create and run the daemonset. |
| `status`<br/>_object_    | The status information of the daemonset.                |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET A DAEMONSET -------------------->

#### Get a daemonset

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/daemonsets/test-aerospike/auth"
```

> The above command returns a JSON structured like this:

```json
{
  "data": {
    "id": "canal/kube-system",
    "metadata": {},
    "spec": {},
    "status": {}
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/daemonsets/:id</code>

Retrieve a daemonset and all its info in a given [environment](#administration-environments).

| Required           | &nbsp;                   |
| ------------------ | ------------------------ |
| `id` <br/>_string_ | The id of the daemonset. |


| Attributes               | &nbsp;                                                  |
| ------------------------ | ------------------------------------------------------- |
| `metadata` <br/>_object_ | The metadata of the daemonset.                          |
| `spec`<br/>_object_      | The specification used to create and run the daemonset. |
| `status`<br/>_object_    | The status information of the daemonset.                |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- CREATE A DAEMONSET -------------------->

#### Create a daemonset

```shell
curl -X POST \
  -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/daemonsets"
  Content-Type: application/json
  {
  "apiVersion": "apps/v1",
  "kind": "DaemonSet",
  "metadata": {
    "name": "daemonset-name",
    "namespace": "default"
  },
  "spec": {
    "selector": {
      "matchLabels": {
        "name": "fluentd-elasticsearch"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "name": "fluentd-elasticsearch"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "fluentd-elasticsearch",
            "image": "quay.io/fluentd_elasticsearch/fluentd:v2.5.2"
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

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/daemonsets</code>

Create a daemonset in a given [environment](#administration-environments).

| Required Attributes           | &nbsp;                                                                    |
| ----------------------------- | ------------------------------------------------------------------------- |
| `apiVersion` <br/> _string_   | The api version (versioned schema) of the daemonset.                      |
| `metadata` <br/>_object_      | The metadata of the daemonset.                                            |
| `metadata.name` <br/>_string_ | The name of the daemonset.                                                |
| `spec`<br/>_object_           | The specification used to create and run the daemonset.                   |
| `spec.selector`<br/>_object_  | The label query over the daemonset's resources.                           |
| `spec.template`<br/>_object_  | The data a daemonset's pod should have when created.                      |
| `spec.spec`<br/>_object_      | The specification used to create and run the pod(s) within the daemonset. |

| Optional Attributes                      | &nbsp;                                                                  |
| ---------------------------------------- | ----------------------------------------------------------------------- |
| `kind`<br/>_string_                      | The string value representing the REST resource this object represents. |
| `metadata.namespace` <br/>_string_       | The namespace in which the daemonset is created.                        |
| `spec.selector.matchLabels`<br/>_object_ | The key value pairs retrieved by a label query from a daemonset.        |

Return value:

| Attributes                 | &nbsp;                                             |
| -------------------------- | -------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the create daemonset task. |
| `taskStatus` <br/>_string_ | The status of the operation.                       |

<!-------------------- DELETE A DAEMONSET -------------------->

#### Delete a daemonset

```shell
curl -X DELETE \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/daemonsets/nginx-ingress-controller/ingress-nginx"
```

> The above command returns a JSON structured like this:

```json
{
  "taskId": "1542bd45-4732-419b-87b6-4ea6ec695c2b",
  "taskStatus": "PENDING"
}
```

<code>DELETE /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/daemonsets/:id</code>

Delete a daemonset from a given [environment](#administration-environments).

| Required           | &nbsp;                   |
| ------------------ | ------------------------ |
| `id` <br/>_string_ | The id of the daemonset. |

Return value:

| Attributes                 | &nbsp;                                             |
| -------------------------- | -------------------------------------------------- |
| `taskId` <br/>_string_     | The id corresponding to the delete daemonset task. |
| `taskStatus` <br/>_string_ | The status of the operation.                       |
