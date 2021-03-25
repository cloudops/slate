## Firewall Rules

### Create a firewall rule

Restrict access to a site using allow and block rules.

<code>POST /services/<a href="#administration-service-connections">:service_code</a>/<a href="#administration-environments">:environment_name</a>/firewallrules?siteId=<a href="#stackpath-sites">:siteId</a></code>

Required Query Params | &nbsp;
---- | -----------
`siteId`<br/>*UUID* | The ID of the site for which to create the firewall rule. This parameter is required.

Required Body Attribute | &nbsp;
------------------------| -----------
`action`<br/>*string* | Either ALLOW or BLOCK.
`name`<br/>*string* | The name of the rule.
`ipStart`<br/>*string* | The start ip adress for the rule. When no `ipEnd` attribute is provided, the rule only applies for the ip provided in `ipStart`.

Optional Body Attribute | &nbsp;
----------------------- | -----------
`ipEnd`<br/>*string* | There end ip adress for the rule.


```shell
curl -X POST \
   -H "MC-Api-Key: your_api_key" \
   -d "request_body" \
   "https://cloudmc_endpoint/api/v1/services/stackpath/test-area/firewallrules?siteId=f9dea588-d7ab-4f42-b6e6-4b85f273f3db"
```
> Request body example for creating a firewall rule:

```js
{
    action: "ALLOW",
    name: "firewall rule",
    ipStart: "192.168.0.6",
    ipEnd: "192.168.0.7"
}
```

The following attributes are returned as part of the response.

Attributes | &nbsp;
------- | -----------
`taskId` <br/>*string* | The task id related to creation of the firewall rule.
`taskStatus` <br/>*string* | The status of the operation.
