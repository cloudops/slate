### Releases


<!-------------------- LIST RELEASES -------------------->

#### List releases

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/releases?cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
```
> The above command returns a JSON structured like this:

```json
{
  "data": [
    {
      "name": "my-aerospike",
      "info": {
        "first_deployed": "2020-01-20T09:35:02.267449-05:00",
        "last_deployed": "2020-01-20T09:35:02.267449-05:00",
        "deleted": "",
        "description": "Install complete",
        "status": "installed",
        "notes": "The Aerospike can be accessed via port 3000 on the following DNS name from within your cluster:\n\n  my-aerospike.default.svc.cluster.local\n\nYou can connect to aeropike in your local machine using port-forwarding:\n\n  export POD_NAME=$(kubectl get pods --namespace default -l \"app=aerospike,release=my-aerospike\" -o jsonpath=\"{.items[0].metadata.name}\")\n  kubectl  --namespace default port-forward $POD_NAME 3000:3000\n"
      },
      "chart": {
        "metadata": {
          "name": "aerospike",
          "home": "http://aerospike.com",
          "sources": [
            "https://github.com/aerospike/aerospike-server"
          ],
          "version": "0.3.2",
          "description": "A Helm chart for Aerospike in Kubernetes",
          "keywords": [
            "aerospike",
            "big-data"
          ],
          "maintainers": [
            {
              "name": "kavehmz",
              "email": "kavehmz@gmail.com"
            },
            {
              "name": "okgolove",
              "email": "okgolove@markeloff.net"
            }
          ],
          "icon": "https://s3-us-west-1.amazonaws.com/aerospike-fd/wp-content/uploads/2016/06/Aerospike_square_logo.png",
          "apiVersion": "v1",
          "appVersion": "v4.5.0.5",
          "deprecated": false
        },
        "values": {
          "annotations": {},
          "args": [],
          "command": [],
          "confFile": "#default config file\nservice {\n    user root\n    group root\n    paxos-protocol v5\n    paxos-single-replica-limit 1\n    pidfile /var/run/aerospike/asd.pid\n    service-threads 4\n    transaction-queues 4\n    transaction-threads-per-queue 4\n    proto-fd-max 15000\n}\n\nlogging {\n    file /var/log/aerospike/aerospike.log {\n        context any info\n    }\n\n    console {\n        context any info\n    }\n}\n\nnetwork {\n    service {\n        address any\n        port 3000\n    }\n\n    heartbeat {\n        address any\n        interval 150\n        #REPLACE_THIS_LINE_WITH_MESH_CONFIG\n        mode mesh\n        port 3002\n        timeout 20\n        protocol v3\n    }\n\n    fabric {\n        port 3001\n    }\n\n    info {\n        port 3003\n    }\n}\n\nnamespace test {\n    replication-factor 2\n    memory-size 1G\n    default-ttl 5d\n    storage-engine device {\n        file /opt/aerospike/data/test.dat\n        filesize 4G\n    }\n}",
          "image": {
            "pullPolicy": "IfNotPresent",
            "repository": "aerospike/aerospike-server",
            "tag": "4.5.0.5"
          },
          "labels": {},
          "metrics": {
            "serviceMonitor": {}
          },
          "nodeSelector": {},
          "persistentVolume": {},
          "replicaCount": 1.0,
          "resources": {},
          "service": {
            "annotations": {},
            "clusterIP": "None",
            "nodePort": {},
            "type": "ClusterIP"
          },
          "terminationGracePeriodSeconds": 30.0,
          "tolerations": []
        }
      },
      "version": 1,
      "namespace": "default"
    }
  ],
  "metadata": {
    "recordCount": 1
  }
}
```



<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases?cluster_id=:cluster_id</code>

Or

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases?namespace=default&cluster_id=:cluster_id</code>



Retrieve a list of all releases in a given [environment](#administration-environments).

Required | &nbsp;
------- | -----------
`cluster_id` <br/>*string* | The id of the cluster in which to list the releases.



Optional | &nbsp;
------- | -----------
`namespace` <br/>*string* | The namespace to list the release. This needs the exact value.


Attributes | &nbsp;
------- | -----------
`name` <br/>*string* | The name of the release.
`info` <br/>*object* | The information about the release.
`info.first_deployed` <br/>*string* | The annotations of the pod.
`info.last_deployed` <br/>*string* | The date of creation of the pod as a string.
`info.deleted` <br/>*string* | The labels associated to the pod.
`info.description` <br/>*string* | The name of the pod.
`info.status` <br/>*string* | The status of the release. Possible values are unknown, installed, uninstalled, superseded, failed, uninstalling, pending-install, pending-upgrade, pending-rollback.
`info.notes` <br/>*string* | The notes linked to the release.
`chart`<br/>*object* | The information related to the chart of used in the release.
`chart.version` <br/>*string* | The version of the chart.
`chart.metadata` <br/>*object* | The metadata associated to the chart.
`chart.metadata.name` <br/>*string* | The name of the chart.
`chart.metadata.home` <br/>*string* | The home URL for the chart.
`chart.metadata.sources` <br/>*list* | The list of source of the charts.
`chart.metadata.version` <br/>*string* | The version of the chart.
`chart.metadata.description` <br/>*string* | The description of the chart.
`chart.metadata.keywords` <br/>*list* | The list of keywords linked to the chart.
`chart.metadata.maintainers` <br/>*list* | The list of the maintainer contact information.
`chart.metadata.icon` <br/>*string* | The icon URL for the chart.
`chart.metadata.appVersion` <br/>*string* | The version of the application.
`chart.metadata.deprecate` <br/>*bool* | If the chart is deprecated or not of the application.
`values` <br/>*object* | All values that were used to install the release.
`version`<br/>*string* | The revision of the release.
`namespace`<br/>*string* | The namespace to which the release is installed.

The information is not totally returned in the list. We filter out the manifest portion. We also filter out the files and the templates of the chart details. This information will be present in the GET request for an individual release.


<!-------------------- GET RELEASE -------------------->

#### Get release

```shell
curl -X GET \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/releases/pspensieri/aerospike-1579797954?cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
```
> The above command returns a JSON structured like this:

```json
{
  "data": {
    "id": "pspensieri/aerospike-1579797954",
    "name": "aerospike-1579797954",
    "info": {
      "first_deployed": "2020-01-23T11:45:57.255189-05:00",
      "last_deployed": "2020-01-24T19:06:12.956425-05:00",
      "deleted": "",
      "description": "Rollback to 2",
      "status": "installed",
      "notes": "The Aerospike can be accessed via port 3000 on the following DNS name from within your cluster:\n\n  aerospike-1579797954.pspensieri.svc.cluster.local\n\nYou can connect to aeropike in your local machine using port-forwarding:\n\n  export POD_NAME=$(kubectl get pods --namespace pspensieri -l \"app=aerospike,release=aerospike-1579797954\" -o jsonpath=\"{.items[0].metadata.name}\")\n  kubectl  --namespace pspensieri port-forward $POD_NAME 3000:3000\n"
    },
    "chart": {
      "metadata": {
        "name": "aerospike",
        "home": "http://aerospike.com",
        "sources": [
          "https://github.com/aerospike/aerospike-server"
        ],
        "version": "0.3.2",
        "description": "A Helm chart for Aerospike in Kubernetes",
        "keywords": [
          "aerospike",
          "big-data"
        ],
        "maintainers": [
          {
            "name": "kavehmz",
            "email": "kavehmz@gmail.com"
          },
          {
            "name": "okgolove",
            "email": "okgolove@markeloff.net"
          }
        ],
        "icon": "https://s3-us-west-1.amazonaws.com/aerospike-fd/wp-content/uploads/2016/06/Aerospike_square_logo.png",
        "apiVersion": "v1",
        "appVersion": "v4.5.0.5",
        "deprecated": false
      },
      "templates": [
        {
          "name": "templates/NOTES.txt",
          "data": "VGhlIEFlcm9zcGlrZSBjYW4"
        },
        {
          "name": "templates/_helpers.tpl",
          "data": "e3svKiB2aW06IHNldCBmaW"
        },
        {
          "name": "templates/configmap.yaml",
          "data": "YXBpVmVyc2lvbjogdjEKa2lu"
        },
        {
          "name": "templates/nodeport.yaml",
          "data": "e3stIGlmIC5WYWx1ZXMuc"
        },
        {
          "name": "templates/service.yaml",
          "data": "YXBpVmVyc2lvbjogdjEKa"
        },
        {
          "name": "templates/servicemonitor.yaml",
          "data": "e3stIGlmIGFuZCAoLlZ"
        },
        {
          "name": "templates/statefulset.yaml",
          "data": "YXBpVmVyc2lvbjogYXBwcy92MQpra"
        }
      ],
      "values": {
        "annotations": {},
        "args": [],
        "command": [],
        "confFile": "#default config file\nservice {\n    user root\n    group root\n    paxos-protocol v5\n    paxos-single-replica-limit 1\n    pidfile /var/run/aerospike/asd.pid\n    service-threads 4\n    transaction-queues 4\n    transaction-threads-per-queue 4\n    proto-fd-max 15000\n}\n\nlogging {\n    file /var/log/aerospike/aerospike.log {\n        context any info\n    }\n\n    console {\n        context any info\n    }\n}\n\nnetwork {\n    service {\n        address any\n        port 3000\n    }\n\n    heartbeat {\n        address any\n        interval 150\n        #REPLACE_THIS_LINE_WITH_MESH_CONFIG\n        mode mesh\n        port 3002\n        timeout 20\n        protocol v3\n    }\n\n    fabric {\n        port 3001\n    }\n\n    info {\n        port 3003\n    }\n}\n\nnamespace test {\n    replication-factor 2\n    memory-size 1G\n    default-ttl 5d\n    storage-engine device {\n        file /opt/aerospike/data/test.dat\n        filesize 4G\n    }\n}",
        "image": {
          "pullPolicy": "IfNotPresent",
          "repository": "aerospike/aerospike-server",
          "tag": "4.5.0.5"
        },
        "labels": {},
        "metrics": {
          "serviceMonitor": {}
        },
        "nodeSelector": {},
        "persistentVolume": {},
        "replicaCount": 1.0,
        "resources": {},
        "service": {
          "annotations": {},
          "clusterIP": "None",
          "nodePort": {},
          "type": "ClusterIP"
        },
        "terminationGracePeriodSeconds": 30.0,
        "tolerations": []
      },
      "files": [
        {
          "name": ".helmignore",
          "data": "IyBQYXR0ZXJucyB0by"
        },
        {
          "name": "OWNERS",
          "data": "YXBwcm92ZXJzOgotIG9rZ29sb3ZlCnJldmlld2VyczoKLSBva2dvbG92ZQo="
        },
        {
          "name": "README.md",
          "data": "IyBBZXJvc3Bpa2UgSGVsbSBDa"
        }
      ]
    },
    "manifest": "---\n# Source: aerospike/templates/configmap.yaml\napiVersion: v1\nkind: ConfigMap\nmetadata:\n  name: aerospike-1579797954\n  labels:\n    app: aerospike\n    chart: aerospike-0.3.2\n    release: aerospike-1579797954\n    heritage: Helm\ndata:\n  aerospike.conf: |\n    # aerospike configuration\n        #default config file\n    service {\n        user root\n        group root\n        paxos-protocol v5\n        paxos-single-replica-limit 1\n        pidfile /var/run/aerospike/asd.pid\n        # HERE UPDATE changed service threads from 4 to 3\n        service-threads 3\n        transaction-queues 4\n        transaction-threads-per-queue 4\n        proto-fd-max 15000\n    }\n    \n    logging {\n        file /var/log/aerospike/aerospike.log {\n            context any info\n        }\n    \n        console {\n            context any info\n        }\n    }\n    \n    network {\n        service {\n            address any\n            port 3000\n        }\n    \n        heartbeat {\n            address any\n            interval 150\n            \n        mesh-seed-address-port aerospike-1579797954-0.aerospike-1579797954 3002\n            mode mesh\n            port 3002\n            timeout 20\n            protocol v3\n        }\n    \n        fabric {\n            port 3001\n        }\n    \n        info {\n            port 3003\n        }\n    }\n    \n    namespace test {\n        replication-factor 2\n        memory-size 1G\n        default-ttl 5d\n        storage-engine device {\n            file /opt/aerospike/data/test.dat\n            filesize 4G\n        }\n    }\n---\n# Source: aerospike/templates/service.yaml\napiVersion: v1\nkind: Service\nmetadata:\n  name: aerospike-1579797954\n  labels:\n    app: aerospike\n    chart: aerospike-0.3.2\n    release: aerospike-1579797954\n    heritage: Helm\n  annotations:\nspec:\n  # so the mesh peer-finder works\n  publishNotReadyAddresses: true\n  \n  clusterIP: \"None\"\n  \n  type: ClusterIP\n  ports:\n    - port: 3000\n      protocol: TCP\n      name: client\n    - port: 3002\n      protocol: TCP\n      name: mesh\n    \n  selector:\n    app: aerospike\n    release: aerospike-1579797954\n---\n# Source: aerospike/templates/statefulset.yaml\napiVersion: apps/v1\nkind: StatefulSet\nmetadata:\n  name: aerospike-1579797954\n  labels:\n    app: aerospike\n    chart: aerospike-0.3.2\n    release: aerospike-1579797954\n    heritage: Helm\nspec:\n  serviceName: aerospike-1579797954\n  replicas: 1\n  selector:\n    matchLabels:\n      app: aerospike\n      release: aerospike-1579797954\n  template:\n    metadata:\n      labels:\n        app: aerospike\n        release: aerospike-1579797954\n      annotations:\n        checksum/config: a070d13fbcb5b721657425639577690b36bcd60897798a9e979ea6c2a2fa24c2\n    spec:\n      terminationGracePeriodSeconds: 30\n      containers:\n      - name: aerospike-1579797954\n        image: \"aerospike/aerospike-server:4.5.0.5\"\n        imagePullPolicy: IfNotPresent\n        \n        \n        ports:\n        - containerPort: 3000\n          name: clients\n        - containerPort: 3002\n          name: mesh\n        - containerPort: 3003\n          name: info\n        readinessProbe:\n          tcpSocket:\n              port: 3000\n          initialDelaySeconds: 15\n          timeoutSeconds: 1\n        volumeMounts:\n        - name: config-volume\n          mountPath: /etc/aerospike\n        resources:\n          \n          {}\n      \n      volumes:\n      - name: config-volume\n        configMap:\n          name: aerospike-1579797954\n          items:\n          - key: aerospike.conf\n            path: aerospike.conf\n      \n  volumeClaimTemplates:\n",
    "version": 4,
    "namespace": "pspensieri",
    "chartVersion": "aerospike / 0.3.2"
  }
}
```

<code>GET /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases?cluster_id=:cluster_id</code>

Retrieve a release in a given [environment](#administration-environments).

Required | &nbsp;
------- | -----------
`cluster_id` <br/>*string* | The id of the cluster in which to list the releases.


Attributes | &nbsp;
------- | -----------
`name` <br/>*string* | The name of the release.
`info` <br/>*object* | The information about the release.
`info.first_deployed` <br/>*string* | The annotations of the pod.
`info.last_deployed` <br/>*string* | The date of creation of the pod as a string.
`info.deleted` <br/>*string* | The labels associated to the pod.
`info.description` <br/>*string* | The name of the pod.
`info.status` <br/>*string* | The status of the release. Possible values are unknown, installed, uninstalled, superseded, failed, uninstalling, pending-install, pending-upgrade, pending-rollback.
`info.notes` <br/>*string* | The notes linked to the release.
`chart`<br/>*object* | The information related to the chart of used in the release.
`chart.version` <br/>*string* | The version of the chart.
`chart.metadata` <br/>*object* | The metadata associated to the chart.
`chart.metadata.name` <br/>*string* | The name of the chart.
`chart.metadata.home` <br/>*string* | The home URL for the chart.
`chart.metadata.sources` <br/>*list* | The list of source of the charts.
`chart.metadata.version` <br/>*string* | The version of the chart.
`chart.metadata.description` <br/>*string* | The description of the chart.
`chart.metadata.keywords` <br/>*list* | The list of keywords linked to the chart.
`chart.metadata.maintainers` <br/>*list* | The list of the maintainer contact information.
`chart.metadata.icon` <br/>*string* | The icon URL for the chart.
`chart.metadata.appVersion` <br/>*string* | The version of the application.
`chart.metadata.deprecate` <br/>*bool* | If the chart is deprecated or not of the application.
`chart.templates` <br/> *list* | The list of templates contained inside the chart.
`chart.templates.name` <br/> *string* | The path name of the template inside the chart.
`chart.templates.data` <br/> *string* | The contents of the template. This is a base64 encode string.
`chart.files` <br/> *list* | The list of files contained inside the chart. These are not YAML files unlike the templates.
`chart.files.name` <br/> *string* | The path name of the file inside the chart.
`chart.files.data` <br/> *string* | The contents of the file. This is a base64 encode string.
`manifest` <br/> *string* | The YAML Kubernetes resources created by the Helm templating.
`values` <br/>*object* | All values that were used to install the release.
`version`<br/>*string* | The revision of the release.
`namespace`<br/>*string* | The namespace to which the release is installed.

<!-- ROLLBACK RELEASE -->
#### Rollback release to previous revision

```shell
curl -X POST \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/releases/pspensieri/aerospike-1579797954&operation=rollback&cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
```
> The above command returns a JSON structured like this:

```json
{
  "data": {
      "name": "aerospike-1579797954",
      "version": 8,
      "info": {
          "deleted": "",
          "description": "Rollback to 6",
          "status": "deployed",
          ...
      ...
  },
  "taskId": "13943961-4a2c-4439-b7c9-05113d3b593a",
  "taskStatus": "SUCCESS"
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases/:id?operation=rollback&cluster_id=:cluster_id</code>

Rollback a release in a given [environment](#administration-environments) to the previous revision.

Required | &nbsp;
------- | -----------
`cluster_id` <br/>*string* | The id of the cluster in which to rollback the release.

Attributes | &nbsp;
------- | -----------
`data` <br/>*Object* | The release object. See [get release](#get-release) for a description of the release attributes.
`taskId` <br/>*string* | The task id related to the pod rollback.
`taskStatus` <br/>*string* | The status of the operation.

<!-------------------- UPGRADE RELEASE -------------------->
#### Upgrade release

```shell
curl -X POST \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/releases/pspensieri/aerospike-1579797954?operation=upgrade&cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
   -d "request_body"
```
> Request body examples:

```js
// Change to the latest version of a chart
{
  "upgradeChart":  "stable/aerospike"
}

// Change to a specific version of a chart
{
  "upgradeChart" : "https://kubernetes-charts.storage.googleapis.com/aerospike-0.3.2.tgz"
}

// Change the values for the latest version
{
  "upgradeChart" : "stable/aerospike",
  "values": "---\n\"replicaCount\": 3\n"
}
```
> The above commands return JSON structured like this:

```json
{
  "taskId": "c50390c7-9d5b-4af4-a2da-e2a2678a83e8",
  "taskStatus": "SUCCESS"
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases/:id?operation=upgrade&cluster_id=:cluster_id</code>

Upgrade a release in a given [environment](#administration-environments).

Required | &nbsp;
------- | -----------
`cluster_id` <br/>*string* | The id of the cluster in which to upgrade the release.
`upgradeChart` <br/>*string* | The id of the chart to upgrade (repo/name) or the url to the version of the chart to use.

Optional | &nbsp;
------- | -----------
`values` <br/>*string* | YAML structured text that will overwrite the default values for the upgrade/installation of the chart.

Attributes | &nbsp;
------- | -----------
`taskId` <br/>*string* | The task id related to the pod upgrade.
`taskStatus` <br/>*string* | The status of the operation.

<!-- UNINSTALL RELEASE -->
#### Uninstall a release

```shell
curl -X POST \
   -H "MC-Api-Key: your_api_key" \
   "https://cloudmc_endpoint/v1/services/a_service/an_environment/releases/pspensieri/aerospike-1579797954&operation=uninstall&cluster_id=projects/cmc-k8s-enabled-llb/locations/us-central1-a/clusters/standard-cluster-1"
   -d "request_body"
```
> Request body example:

```json
{
   "keepHistory": true
}
```
> The above command returns a JSON structured like this:

```json
{
  "data": {
      "version": 0,
      "keepHistory": false
  },
  "taskId": "938f11b2-b37d-459e-8cf2-dea05c4d8f63",
  "taskStatus": "SUCCESS"
}
```

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/releases/:id?operation=uninstall&cluster_id=:cluster_id</code>

Uninstall a release in a given [environment](#administration-environments).

Required | &nbsp;
------- | -----------
`cluster_id` <br/>*string* | The id of the cluster in which to uninstall the release.

Optional | &nbsp;
------- | -----------
`keepHistory` <br/>*bool* | If true, will keep release history after uninstalling. Defaults to false.

Attributes | &nbsp;
------- | -----------
`version` <br/>*string* | The uninstalled release's revision. Revision 0 indicated it was uninstalled.
`keepHistory` <br/>*string* | The *keepHistory* value used when uninstalling the chart.
`taskId` <br/>*string* | The task id related to the pod uninstall.
`taskStatus` <br/>*string* | The status of the operation.