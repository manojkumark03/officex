---
description: Operations for managing contacts
---

# Contacts

## Get Contact

Retrieve a contact by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/get/{contact_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/xc58af7/drive-org-id-contacts-list?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>        | DriveID\_abc123      |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------- | -------------------- |
| contact\_id <mark style="color:red;">(required)</mark>      | <p></p><p><strong>string (UserID)</strong> </p><p>ID of the contact to retrieve</p> | UserID\_abcdef123456 |

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
            "id": "UserID_c5hjz-wpnfl-3v2jx-hglmv-6y7wm-o6zur-e6q2n-e7vp3-4z762-ajc7l-mqe",
            "name": "manzy",
            "avatar": "",
            "email": "",
            "notifications_url": "",
            "public_note": "",
            "private_note": "",
            "evm_public_address": "",
            "icp_principal": "c5hjz-wpnfl-3v2jx-hglmv-6y7wm-o6zur-e6q2n-e7vp3-4z762-ajc7l-mqe",
            "seed_phrase": "",
            "from_placeholder_user_id": "UserID_c5hjz-wpnfl-3v2jx-hglmv-6y7wm-o6zur-e6q2n-e7vp3-4z762-ajc7l-mqe",
            "redeem_code": "RedeemTokenID_dd090970-fcb1-49bc-af35-69eba1a157f5",
            "created_at": 1755445000597,
            "last_online_ms": 0,
            "external_id": null,
            "external_payload": null,
            "secret_entropy": "",
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ],
            "labels": [],
            "group_previews": [
                {
                    "group_id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                    "invite_id": "GroupInviteID_e8479d67-0806-4ee3-bb75-6ff5245ee21e",
                    "is_admin": false,
                    "group_name": "Group for All",
                    "group_avatar": ""
                }
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

|          | type                                                                                                                              |
| -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestGetContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L331)  |
| Response | [IResponseGetContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L337) |

***

## List Contacts

List contacts with optional filtering and pagination

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/list
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/xc58af7/drive-org-id-contacts-list?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| <p><br>filters </p> | <p><strong>string &#x3C;= 256 characters</strong><br>Default: ""<br>Filter string for contacts</p>     |        |
| ------------------- | ------------------------------------------------------------------------------------------------------ | ------ |
| page\_size          | <p><strong>integer [ 1 .. 1000 ]</strong><br>Default: 50<br>Number of items per page</p>               | 50     |
| direction           | <p><strong>string</strong></p><p>Default: "ASC"</p><p>Enum: "ASC" "DESC"</p><p>Sort direction</p>      | ASC    |
| cursor\_up          | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (previous page)</p> | string |
| cursor\_down        | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (next page)</p>     | string |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
  "filters": "",
  "page_size": 50,
  "direction": "ASC",
  "cursor_up": "string",
  "cursor_down": "string"
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
| Request  | [IRequestListContacts](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L340)  |
| Response | [IResponseListContacts](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L343) |

***

## Create Contact

Create a new contact

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/e9l358o/drive-org-id-contacts-create-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user </p>                                                                          | UserID\_abc123                    |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| name                                          | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the contact</p>                                                                     | John Doe                          |
| avatar                                        | <p><strong>string or null &#x3C;= 2048 characters</strong></p><p>Profile picture URL</p>                                                             |                                   |
| notifications\_url                            | <p><strong>string &#x3C;= 256 characters</strong></p><p>Alternative of email notifications</p>                                                       |                                   |
| email                                         | <p><strong>string or null &#x3C;= 256 characters</strong></p><p>Primary email for the contact</p>                                                    |                                   |
| evm\_public\_address                          | <p><strong>string (EvmPublicAddress)</strong></p><p>EVM public address.  </p>                                                                        |                                   |
| public\_note                                  | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the contact</p>                                                   | Project manager for Alpha group   |
| private\_note                                 | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the contact</p>                                                  | Primary contact for urgent issues |
| external\_id                                  | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                |                                   |
| external\_payload                             | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> |                                   |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "UserID_67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae",
            "name": "John Doe",
            "avatar": "",
            "email": "",
            "notifications_url": "",
            "public_note": "Project manager for Alpha group",
            "private_note": "Primary contact for urgent issues",
            "evm_public_address": "",
            "icp_principal": "67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae",
            "seed_phrase": "",
            "secret_entropy": "",
            "labels": [],
            "created_at": 1755445239883,
            "last_online_ms": 0,
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ],
            "group_previews": [
                {
                    "group_id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                    "invite_id": "GroupInviteID_c9b969bf-5a53-4f27-86eb-2c8c803dd4dd",
                    "is_admin": false,
                    "group_name": "Group for All",
                    "group_avatar": ""
                }
            ]
        }
    }
}
```



</details>

<details>

<summary><mark style="color:red;">error</mark></summary>

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

|          | type                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestCreateContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L347)  |
| Response | [IResponseCreateContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L379) |

***

## Update Contact

Update a contact'

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/jw7a1iq/drive-org-id-contacts-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user </p>                                                                          | UserID\_67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae                             |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| name                                          | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the contact</p>                                                                     | Johnny the Kid, Doe                                                                                 |
| avatar                                        | <p><strong>string or null &#x3C;= 2048 characters</strong></p><p>Profile picture URL</p>                                                             |                                                                                                     |
| notifications\_url                            | <p><strong>string &#x3C;= 256 characters</strong></p><p>Alternative of email notifications</p>                                                       |                                                                                                     |
| email                                         | <p><strong>string or null &#x3C;= 256 characters</strong></p><p>Primary email for the contact</p>                                                    |                                                                                                     |
| evm\_public\_address                          | <p><strong>string (EvmPublicAddress)</strong></p><p>EVM public address.  </p>                                                                        |                                                                                                     |
| public\_note                                  | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the contact</p>                                                   | Senior Project Manager for Bark Group                                                               |
| private\_note                                 | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the contact</p>                                                  | Recently promoted, great communicator                                                               |
| external\_id                                  | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                |                                                                                                     |
| external\_payload                             | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | "{"department": "product", "title": "Lead Project Manager", "location": "Remote", "updated": true}" |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "UserID_67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae",
            "name": "Johnny the Kid, Doe",
            "avatar": "",
            "email": "",
            "notifications_url": "",
            "public_note": "Senior Project Manager for Bark Group",
            "private_note": "Recently promoted, great communicator",
            "evm_public_address": "",
            "icp_principal": "67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae",
            "seed_phrase": "",
            "from_placeholder_user_id": null,
            "redeem_code": null,
            "created_at": 1755445239883,
            "last_online_ms": 0,
            "external_id": "",
            "external_payload": "{\"department\": \"product\", \"title\": \"Lead Project Manager\", \"location\": \"Remote\", \"updated\": true}",
            "secret_entropy": "",
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ],
            "labels": [],
            "group_previews": [
                {
                    "group_id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                    "invite_id": "GroupInviteID_c9b969bf-5a53-4f27-86eb-2c8c803dd4dd",
                    "is_admin": false,
                    "group_name": "Group for All",
                    "group_avatar": ""
                }
            ]
        }
    }
}
```



</details>

<details>

<summary><mark style="color:red;">error</mark></summary>

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

|          | type                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestUpdateContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L382)  |
| Response | [IResponseUpdateContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L405) |



## Delete Contact

Delete an existing contact

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/uuupy39/drive-org-id-contacts-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user </p> | UserID\_67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae |
| --------------------------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "UserID_67q5a-2manu-6wyl6-6onic-pvqe4-bydge-lhy4g-22nvo-hcact-5qmki-yae",
            "deleted": true
        }
    }
}
```



</details>

<details>

<summary><mark style="color:red;">error</mark></summary>

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

|          | type                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestDeleteContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L408)  |
| Response | [IResponseDeleteContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L414) |

### Redeem a Contact

Redeems a contact and superswap replace the old user id

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/contacts/redeem
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/8epob6k/drive-org-id-groups-invites-redeem?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| current\_user\_id  | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user </p>                         | UserID\_ocjx7-nigdl-juj3n-5m3cu-2c7g3-hyqrv-hupit-c76dw-dnc67-slomg-hqe |
| ------------------ | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| new\_user\_id      | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user </p>                         | UserID\_ocjx7-nigdl-juj3n-5m3cu-2c7g3-hyqrv-hupit-c76dw-dnc67-slomg-hqe |
| redeem\_code       | <p><strong>string</strong><br>Redemption code to prove authority .it starts with RedeemTokenID_</p> | RedeemTokenID\_0e24ef27-21a6-4ac7-9c13-99ab752a93b9                     |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "contact": {
                "id": "UserID_ocjx7-nigdl-juj3n-5m3cu-2c7g3-hyqrv-hupit-c76dw-dnc67-slomg-hqe",
                "name": "person2",
                "avatar": "",
                "email": "",
                "notifications_url": "",
                "public_note": "",
                "private_note": "",
                "secret_entropy": "",
                "evm_public_address": "",
                "icp_principal": "ocjx7-nigdl-juj3n-5m3cu-2c7g3-hyqrv-hupit-c76dw-dnc67-slomg-hqe",
                "seed_phrase": "",
                "from_placeholder_user_id": "UserID_ghf7e-v6cqw-pupvd-qojec-uz3da-ptqum-i6l3g-y65ry-4f4yq-dejmn-sae",
                "redeem_code": null,
                "created_at": 1755523564446,
                "last_online_ms": 0,
                "external_id": null,
                "external_payload": null,
                "permission_previews": [
                    "CREATE",
                    "VIEW",
                    "EDIT",
                    "DELETE",
                    "INVITE"
                ],
                "labels": [],
                "group_previews": [
                    {
                        "group_id": "GroupID_5d7c60d3-b8dc-4990-9fe7-b81dc9ec7479",
                        "invite_id": "GroupInviteID_be90ddac-95f4-46a5-8a58-a750663516ae",
                        "is_admin": false,
                        "group_name": "Group for All",
                        "group_avatar": ""
                    }
                ]
            },
            "api_key": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiI3YmQ5NGFmOTlhY2ZiNTM5YzNkMTc2OTdhMzFkYzRiYTM5MDc1ZmUzMzk3NWRhZDQ1YTdlOGI4ZTRmYWZmYzg2In0="
        }
    }
}
```



</details>

<details>

<summary><mark style="color:red;">error</mark></summary>

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

|          | type                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestRedeemContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L423)  |
| Response | [IResponseRedeemContact](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L430) |
