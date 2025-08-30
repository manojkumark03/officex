---
description: Operations for managing API keys
---

# API Key

## Get API Key

Retrieve an API key by its ID

<mark style="color:green;background-color:green;">GET</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/api_keys/get/{api_key_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/pm1ausb/drive-org-id-api-keys-get-api-key-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>  | DriveID\_abc123  |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------- |
| api\_key\_id <mark style="color:red;">(required)</mark>     | <p><strong>string (ApiKeyID)</strong></p><p>ID of the API key to retrieve</p> | ApiKeyID\_abc123 |

</details>

<details>

<summary>H<strong>eader Parameters</strong></summary>

| <p><br>Authorization <mark style="color:red;">(required)</mark></p> | <p><strong>stringBearer TOKEN</strong><br>Bearer token for authentication</p> | Bearer eyJhbGciOiJIUz... |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------ |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "ApiKeyID_b9cfb179-f01b-4f23-a9bd-313211815c4c",
            "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJlOWY2M2FhMzc2YWVkMjg2YWJhZWNkZTNhOWFkOTIwZTllN2VmMzhhM2Q4ZGQyNWMwZTcxMTA2NGQ2YjMzYzc3In0=",
            "user_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "name": "My API Key",
            "created_at": 1756124936665,
            "begins_at": 1756124936665,
            "expires_at": -1,
            "is_revoked": 0,
            "external_id": null,
            "external_payload": null,
            "labels": [],
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ]
        }
    }
}
```



</details>

<details>

<summary><mark style="color:$danger;">error</mark></summary>

```json
{
  "err": {
    "code": 0,
    "message": "string"
  }
}
```

</details>

**Typescript Types**

|          | type                                                                                                                             |
| -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestGetApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L253)  |
| Response | [IResponseGetApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L259) |

***

## List API Keys

List all API keys for a specific user

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/api_keys/list/{user_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/o7hfbim/drive-org-id-api-keys-list-user-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>  | DriveID\_abc123  |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------- | ---------------- |
| api\_key\_id <mark style="color:red;">(required)</mark>     | <p><strong>string (ApiKeyID)</strong></p><p>ID of the API key to retrieve</p> | ApiKeyID\_abc123 |

</details>

<details>

<summary>H<strong>eader Parameters</strong></summary>

| <p><br>Authorization <mark style="color:red;">(required)</mark></p> | <p><strong>stringBearer TOKEN</strong><br>Bearer token for authentication</p> | Bearer eyJhbGciOiJIUz... |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------ |



</details>

<details>

<summary><strong>Request Body schema</strong></summary>

| user\_id | <p><strong>string (UserID)</strong><br>Unique identifier for a user</p> | UserID\_abc123 |
| -------- | ----------------------------------------------------------------------- | -------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": [
            {
                "id": "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957",
                "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJjMjZmYTNhZGQ5NGMxMWVjNjY3Njk2OWIxOGRiOTZiNmNmYTI0Y2ZhZmYwYjI0MGY0ZDU4MmFhOTI0NTlkNTA5In0=",
                "user_id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                "name": "My API Key",
                "created_at": 1756124773388,
                "begins_at": 1756124773388,
                "expires_at": -1,
                "is_revoked": 0,
                "external_id": null,
                "external_payload": null,
                "labels": [],
                "permission_previews": [
                    "CREATE",
                    "VIEW",
                    "EDIT",
                    "DELETE",
                    "INVITE"
                ]
            }
        ]
    }
}
```



</details>

<details>

<summary><mark style="color:$danger;">error</mark></summary>

```json
{
  "err": {
    "code": 0,
    "message": "string"
  }
}
```

</details>

**Typescript Types**

|          | type                                                                                                                               |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestListApiKeys](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L262)  |
| Response | [IResponseListApiKeys](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L268) |

***

## Create API Key

Create a new API key

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/api_keys/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/uq7kh7z/drive-org-id-api-keys-create?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>H<strong>eader Parameters</strong></summary>

| <p><br>Authorization <mark style="color:red;">(required)</mark></p> | <p><strong>stringBearer TOKEN</strong><br>Bearer token for authentication</p> | Bearer eyJhbGciOiJIUz... |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------ |



</details>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p> | DriveID\_abc123 |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------- |

</details>

<details>

<summary><strong>Request Body schema:</strong></summary>

| <p><br>name <mark style="color:red;">(required)</mark></p> | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the API key</p>                                             | Development API Key                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| user\_id                                                   | <p><strong>string (UserID)</strong><br>Unique identifier for a user</p>                                                      | UserID\_abc123                                                    |
| expires\_at                                                | <p><strong>integer or null &#x3C;int64></strong></p><p>Timestamp when the key expires, -1 for never expires</p>              | 1703980800000                                                     |
| external\_id                                               | <p><strong>string or null &#x3C;= 256 characters</strong><br>External identifier</p>                                         | ext-key-001                                                       |
| external\_payload                                          | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Additional data for external systems<br>(Stringified JSON)</p> | "{"department": "engineering", "purpose": "backend-integration"}" |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957",
            "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJjMjZmYTNhZGQ5NGMxMWVjNjY3Njk2OWIxOGRiOTZiNmNmYTI0Y2ZhZmYwYjI0MGY0ZDU4MmFhOTI0NTlkNTA5In0=",
            "user_id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
            "name": "My API Key",
            "created_at": 1756124773388,
            "is_revoked": false,
            "begins_at": 1756124773388,
            "expires_at": -1,
            "labels": [],
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ]
        }
    }
}
```



</details>

<details>

<summary><mark style="color:$danger;">error</mark></summary>

```json
{
  "err": {
    "code": 0,
    "message": "string"
  }
}
```

</details>

**Typescript Types**

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCreateApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L271)  |
| Response | [IResponseCreateApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L288) |

***

## Update API Key

Update API key

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/api_keys/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/6xdxpxr/drive-org-id-api-keys-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>H<strong>eader Parameters</strong></summary>

| <p><br>Authorization <mark style="color:red;">(required)</mark></p> | <p><strong>stringBearer TOKEN</strong><br>Bearer token for authentication</p> | Bearer eyJhbGciOiJIUz... |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------ |



</details>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p> | DriveID\_abc123 |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------- |

</details>

<details>

<summary><strong>Request Body schema</strong></summary>

| id <mark style="color:red;">(required)</mark> | <p><strong>string (ApiKeyID)</strong><br>Unique identifier for an API key</p>                                                          | ApiKeyID\_b9cfb179-f01b-4f23-a9bd-...                             |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| <p><br>name</p>                               | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the API key</p>                                                       | Development API Key                                               |
| begins\_at                                    | **integer or null** Timestamp when the key begins                                                                                      | 0                                                                 |
| expires\_at                                   | <p><strong>integer or null &#x3C;int64></strong></p><p>Timestamp when the key expires, -1 for never expires</p>                        | -1                                                                |
| is\_revoked                                   | <p><strong>boolean or null</strong></p><p>Whether to revoke the API key</p>                                                            | false                                                             |
| external\_id                                  | <p><strong>string or null &#x3C;= 256 characters</strong><br>External identifier</p>                                                   | ext-key-001                                                       |
| external\_payload                             | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Additional data for external integrations. </p><p>(Stringified JSON)</p> | "{"department": "engineering", "purpose": "backend-integration"}" |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "ApiKeyID_b9cfb179-f01b-4f23-a9bd-313211815c4c",
            "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJlOWY2M2FhMzc2YWVkMjg2YWJhZWNkZTNhOWFkOTIwZTllN2VmMzhhM2Q4ZGQyNWMwZTcxMTA2NGQ2YjMzYzc3In0=",
            "user_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "name": "My API Key",
            "private_note": null,
            "created_at": 1756124936665,
            "begins_at": 1756124936665,
            "expires_at": -1,
            "is_revoked": 0,
            "external_id": null,
            "external_payload": null,
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ]
        }
    }
}
```



</details>

<details>

<summary><mark style="color:$danger;">error</mark></summary>

```json
{
  "err": {
    "code": 0,
    "message": "string"
  }
}
```

</details>

**Typescript Types**

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestUpdateApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L291)  |
| Response | [IResponseUpdateApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L309) |

***

## Delete API Key

Delete an existing API key

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/api_keys/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ui0f9zg/drive-org-id-api-keys-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>H<strong>eader Parameters</strong></summary>

| <p><br>Authorization <mark style="color:red;">(required)</mark></p> | <p><strong>stringBearer TOKEN</strong><br>Bearer token for authentication</p> | Bearer eyJhbGciOiJIUz... |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------ |



</details>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p> | DriveID\_abc123 |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------- |

</details>

<details>

<summary><strong>Request Body schema</strong></summary>

| id <mark style="color:red;">(required)</mark> | <p><strong>string (ApiKeyID)</strong><br>Unique identifier for an API key</p> | ApiKeyID\_abc123 |
| --------------------------------------------- | ----------------------------------------------------------------------------- | ---------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "ok": {
                "data": {
                    "id": "ApiKeyID_b9cfb179-f01b-4f23-a9bd-313211815c4c",
                    "deleted": true
                }
            }
        }
    }
}
```



</details>

<details>

<summary><mark style="color:$danger;">error</mark></summary>

```json
{
  "err": {
    "code": 0,
    "message": "string"
  }
}
```

</details>

**Typescript Types**

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDeleteApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L312)  |
| Response | [IResponseDeleteApiKey](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L318) |
