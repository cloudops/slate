### Ingresses

<!-------------------- LIST INGRESSES -------------------->

#### List ingresses

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/ingresses"
```

> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "id": "cloudmc/cmc-stg",
      "endpoint": "http://cmc.cloudmc-staging-endpoint.com",
      "service": {
        "port": "8080",
        "name": "cloudmc"
      },
      "metadata": {
        "annotations": {},
        "creationTimestamp": "2019-07-11T10:00:18.000-04:00",
        "generation": 10,
        "name": "cloudmc",
        "namespace": "cmc-stg",
        "resourceVersion": "143213903",
        "selfLink": "/apis/extensions/v1beta1/namespaces/cmc-stg/ingresses/cloudmc",
        "uid": "376bc4c5-a3e4-11e9-b6bd-02006e76001e"
      },
      "spec": {
        "rules": [],
        "tls": []
      },
      "status": {
        "loadBalancer": {}
      }
    },
    {
      "id": "cm-acme-http-solver-75png/auth",
      "endpoint": "http://cmc.cloudmc-staging-endpoint.com",
      "service": {
        "port": "8089",
        "name": "cm-acme-http-solver-2x5gv"
      },
      "metadata": {
        "annotations": {},
        "creationTimestamp": "2020-06-24T11:00:49.000-04:00",
        "generateName": "cm-acme-http-solver-",
        "generation": 1,
        "labels": {
          "acme.cert-manager.io/http-domain": "1965164889",
          "acme.cert-manager.io/http-token": "820448657",
          "acme.cert-manager.io/http01-solver": "true"
        },
        "name": "cm-acme-http-solver-75png",
        "namespace": "auth",
        "ownerReferences": [],
        "resourceVersion": "143213968",
        "selfLink": "/apis/extensions/v1beta1/namespaces/auth/ingresses/cm-acme-http-solver-75png",
        "uid": "48720f48-f2bc-45fc-95c5-60cae8ffe11e"
      },
      "spec": {
        "rules": []
      },
      "status": {
        "loadBalancer": {}
      }
    }
  ]
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/ingresses</code>

Retrieve a list of all ingresses in a given [environment](#administration-environments).

| Attributes                                 | &nbsp;                                                          |
| ------------------------------------------ | --------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the ingress.                                          |
| `endpoint` <br/>_string_                   | The endpoint of the ingress.                                    |
| `service` <br/>_object_                    | The service associated with the ingress.                        |
| `service.port` <br/>_string_               | The port of the service associated with the ingress.            |
| `service.name` <br/>_string_               | The name of the service associated with the ingress.            |
| `metadata` <br/>_object_                   | The metadata of the ingress.                                    |
| `metadata.name` <br/>_string_              | The name of the ingress.                                        |
| `metadata.namespace` <br/>_string_         | The namespace in which the ingress is created.                  |
| `metadata.labels` <br/>_object_            | The labels associated with the ingress.                         |
| `metadata.uid` <br/>_object_               | The UUID of the ingress.                                        |
| `spec`<br/>_object_                        | The attributes that a user specifies for an ingress.            |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET AN INGRESS -------------------->

#### Get an ingress

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/ingresses/cloudmc/cmc-stg"
```

> The above command returns a JSON structured like this:

```json
{
  "data": {
    "id": "cloudmc/cmc-stg",
    "endpoint": "http://cmc.cloudmc-staging-endpoint.com",
    "service": {
      "port": "8080",
      "name": "cloudmc"
    },
    "metadata": {
      "annotations": {},
      "creationTimestamp": "2019-07-11T10:00:18.000-04:00",
      "generation": 10,
      "name": "cloudmc",
      "namespace": "cmc-stg",
      "resourceVersion": "143213903",
      "selfLink": "/apis/extensions/v1beta1/namespaces/cmc-stg/ingresses/cloudmc",
      "uid": "376bc4c5-a3e4-11e9-b6bd-02006e76001e"
    },
    "spec": {
      "rules": [],
      "tls": []
    },
    "status": {
      "loadBalancer": {}
    }
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/ingresses/:id</code>

Retrieve an ingress and all its info in a given [environment](#administration-environments).

| Attributes                                 | &nbsp;                                                          |
| ------------------------------------------ | --------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the ingress.                                          |
| `endpoint` <br/>_string_                   | The endpoint of the ingress.                                    |
| `service` <br/>_object_                    | The service associated with the ingress.                        |
| `service.port` <br/>_string_               | The port of the service associated with the ingress.            |
| `service.name` <br/>_string_               | The name of the service associated with the ingress.            |
| `metadata` <br/>_object_                   | The metadata of the ingress.                                    |
| `metadata.name` <br/>_string_              | The name of the ingress.                                        |
| `metadata.namespace` <br/>_string_         | The namespace in which the ingress is created.                  |
| `metadata.labels` <br/>_object_            | The labels associated with the ingress.                         |
| `metadata.uid` <br/>_object_               | The UUID of the ingress.                                        |
| `spec`<br/>_object_                        | The attributes that a user specifies for an ingress.            |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- CREATE INGRESS -------------------->

#### Create an ingress
```shell
curl -X POST \
  -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/ingresses"
  Content-Type: application/json
  {
  "apiVersion": "networking.k8s.io/v1beta1",
  "kind": "Ingress",
  "metadata": {
    "name": "ingress-name",
    "namespace": "default",
    "annotations": {
      "nginx.ingress.kubernetes.io/rewrite-target": "/"
    }
  },
  "spec": {
    "rules": [
      {
        "hostname": "endpoint.com",
        "http": {
          "paths": [
            {
              "path": "/testpath",
              "pathType": "Prefix",
              "backend": {
                "serviceName": "test",
                "servicePort": 80
              }
            }
          ]
        }
      }
    ]
  }
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/ingresses</code>

Create an ingress in a given [environment](#administration-environments).

| Required Attributes                        | &nbsp;                                                                  |
| ------------------------------------------ | ------------------------------------------------------------------------|
| `apiVersion` <br/> _string_                | The api version (versioned schema) of the ingress.                      |
| `metadata` <br/>_object_                   | The metadata of the ingress.                                            |
| `metadata.name` <br/>_string_              | The name of the ingress.                                                |
| `spec`<br/>_object_                        | The specification used to create and run the ingress.                   |
| `spec.rules`<br/>_object_                  | The list of host rules used to configure the ingress.                   |

| Optional Attributes                        | &nbsp;                                                                  |
| ------------------------------------------ | ------------------------------------------------------------------------|
| `kind`<br/>_string_                        | The string value of the REST resource that this object represents.      |
| `metadata.namespace` <br/>_string_         | The namespace in which the ingress is created.                          |

Return value:

| Attributes                 | &nbsp;                                           |
---------------------------- | -------------------------------------------------|
| `taskId` <br/>_string_     | The id corresponding to the create ingress task. |
| `taskStatus` <br/>_string_ | The status of the operation.                     |