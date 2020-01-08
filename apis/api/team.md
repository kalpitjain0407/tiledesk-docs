

{% api-method method="get" host="https://api.tiledesk.com" path="/v1/:project\_id/project_users" %}
{% api-method-summary %}
Get the team
{% endapi-method-summary %}

{% api-method-description %}
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="project\_id" type="string" required=true %}
the Project Id is a unique code assigned to your project when you create it in Tiledesk.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
authorization token. Basic Auth or JWT
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text
[
   {
      "_id":"5df2240cecd41b00173a06bc",
      "id_project":"5df2240cecd41b00173a06bb",
      "id_user":{
         "_id":"5aaa99024c3b110014b478f0",
         "email":"andrea.leo@frontiere21.it",
         "firstname":"Andrea",
         "lastname":"Leo",
         "emailverified":true,
         "__v":0,
         "resetpswrequestid":""
      },
      "role":"owner",
      "user_available":true,
      "createdBy":"5aaa99024c3b110014b478f0",
      "createdAt":"2019-12-12T11:27:08.581Z",
      "updatedAt":"2019-12-12T11:27:08.581Z",
      "__v":0
   },
   {
      "_id":"5df34ab80bc923001792e274",
      "id_project":"5df2240cecd41b00173a06bb",
      "id_user":{
         "_id":"5de9200d6722370017731969",
         "email":"nuovopre@f21test.it",
         "firstname":"Nuovopre",
         "lastname":"Pre",
         "emailverified":false,
         "createdAt":"2019-12-05T15:19:41.296Z",
         "updatedAt":"2019-12-05T15:19:41.296Z",
         "__v":0
      },
      "role":"admin",
      "user_available":true,
      "createdBy":"5aaa99024c3b110014b478f0",
      "createdAt":"2019-12-13T08:24:24.586Z",
      "updatedAt":"2020-01-04T09:45:26.331Z",
      "__v":0
   },
   {
      "_id":"5e09e36d3030640017718ee2",
      "id_project":"5df2240cecd41b00173a06bb",
      "id_user":{
         "_id":"5e09e36d3030640017718edf",
         "email":"magnegerki@enayu.com",
         "firstname":"magnegerki",
         "lastname":"magnegerki",
         "emailverified":false,
         "createdAt":"2019-12-30T11:45:49.123Z",
         "updatedAt":"2019-12-30T11:45:49.123Z",
         "__v":0
      },
      "role":"agent",
      "user_available":false,
      "createdBy":"5aaa99024c3b110014b478f0",
      "createdAt":"2019-12-30T11:45:49.419Z",
      "updatedAt":"2020-01-04T09:45:27.207Z",
      "__v":0
   }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}





