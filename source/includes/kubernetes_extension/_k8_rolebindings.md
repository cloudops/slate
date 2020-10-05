#### Role bindings

<!-------------------- LIST ROLE BINDINGS -------------------->

##### List (namespace) role bindings

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/rolebindings?cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
```

> The above command returns a JSON structured like this:

```json
{

    "data": {
        "entity": {
          "id": "kubeadm:bootstrap-signer-clusterinfo",
          "age": "1w5d",
          "metadata": {
            "creationTimestamp": "2020-09-18T10:46:32.000-04:00",
            "name": "kubeadm:bootstrap-signer-clusterinfo",
            "namespace": "kube-public",
            "uid": "4fcfe5b9-a1c3-4b3b-9cb6-6df4a1da945f"
          },
          "roleRef": {
            "apiGroup": "rbac.authorization.k8s.io",
            "kind": "Role",
            "name": "kubeadm:bootstrap-signer-clusterinfo"
          },
          "subjects": [
            {
              "apiGroup": "rbac.authorization.k8s.io",
              "kind": "User",
              "name": "system:anonymous"
            }
          ]
        },
        "fieldTransitions": {},
        "operations": []
      },
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/rolebindings?cluster_id=:cluster_id</code>

Retrieve a list of all role bindings in a given [environment](#administration-environments).

| Attributes                                 | &nbsp;                                                                                       |
| ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| `id` <br/>_string_                         | The id of the role binding.                                                               |                                                    |
| `metadata` <br/>_object_                   | The metadata of the role binding.                                                         |
| `metadata.creationTimestamp` <br/>_string_ | The date of creation of the role binding as a string.                                     |
| `metadata.name` <br/>_string_              | The name of the role binding.                                                             |
| `metadata.namespace` <br/>_string_         | The namespace in which the role binding is created.                                       |
| `metadata.uid` <br/>_object_               | The UUID of the role binding.                                                          |       `subjects`<br/>_array_      | The array of subjects associated with this role binding.                                               |                                             |

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).

<!-------------------- GET A ROLE BINDING -------------------->

##### Get a role binding

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/rolebindings/rolebinding-name/rolebinding-namespace?cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
```

> The above command returns a JSON structured like this:

```json
{

    "data": {

          "id": "kubeadm:bootstrap-signer-clusterinfo",
          "age": "1w5d",
          "metadata": {
            "creationTimestamp": "2020-09-18T10:46:32.000-04:00",
            "name": "kubeadm:bootstrap-signer-clusterinfo",
            "namespace": "kube-public",
            "uid": "4fcfe5b9-a1c3-4b3b-9cb6-6df4a1da945f"
          },
          "roleRef": {
            "apiGroup": "rbac.authorization.k8s.io",
            "kind": "Role",
            "name": "kubeadm:bootstrap-signer-clusterinfo"
          },
          "subjects": [
            {
              "apiGroup": "rbac.authorization.k8s.io",
              "kind": "User",
              "name": "system:anonymous"
            }
          ]
        },
        "fieldTransitions": {},
        "operations": []
      },
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/rolebindings/:id?cluster_id=:cluster_id</code>

Retrieve a role binding and all its info in a given [environment](#administration-environments).

| Attributes                 | &nbsp;                                            |
| -------------------------- | ------------------------------------------------- |
| `id` <br/>_string_         | The id of the role binding.                          |
| `apiVersion` <br/>_string_ | The API version used to retrieve this role binding.  |
| `metadata` <br/>_object_   | The metadata of the role binding.                    |
| `subjects` <br/>_array_       | The array of subjects associated with this role binding.|

Note that the list is not complete, since it is refering to the [kubernetes api details](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md).