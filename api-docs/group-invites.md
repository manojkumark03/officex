---
description: Operations for managing group invites
---

# Group Invites

## Get Group Invite

Retrieve a group invite by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/get/{invite_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/6ulfo6u/drive-org-id-groups-invites-get-invite-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>    | DriveID\_abc123..                                   |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------- |
| invite\_id <mark style="color:red;">(required)</mark>       | <p></p><p><strong>string</strong> </p><p>ID of the group invite to retrieve</p> | GroupInviteID\_9ac42630-fe7b-4272-8e49-381f0109e261 |

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
            "id": "GroupInviteID_9ac42630-fe7b-4272-8e49-381f0109e261",
            "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
            "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "invitee_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "role": "ADMIN",
            "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "active_from": 1755518217882,
            "expires_at": -1,
            "created_at": 1755518217882,
            "last_modified_at": 1755518217882,
            "redeem_code": null,
            "from_placeholder_invitee": null,
            "labels": [],
            "external_id": null,
            "external_payload": null,
            "group_name": "my  group",
            "group_avatar": "",
            "invitee_name": "Owner",
            "invitee_avatar": null,
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

|          | type                                                                                                                                   |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestGetGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1096)  |
| Response | [IResponseGetGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1102) |

***

## List Group Invites

List group invites with optional filtering and pagination

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/list
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ee9jlol/drive-org-id-groups-invites-list?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| group\_id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupID)</strong><br>Unique identifier for a group</p>                              | GroupID\_b810a4d0-55bb-4bbb-84cf-b044e702a10d |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | --------------------------------------------- |
| <p><br>filters </p>                                  | <p><strong>string &#x3C;= 256 characters</strong><br>Default: ""<br>Filter string for groups</p>       |                                               |
| page\_size                                           | <p><strong>integer [ 1 .. 1000 ]</strong><br>Default: 50<br>Number of items per page</p>               | 50                                            |
| direction                                            | <p><strong>string</strong></p><p>Default: "ASC"</p><p>Enum: "ASC" "DESC"</p><p>Sort direction</p>      | ASC                                           |
| cursor\_up                                           | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (previous page)</p> | string                                        |
| cursor\_down                                         | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (next page)</p>     | string                                        |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "items": [
                {
                    "id": "GroupInviteID_9ac42630-fe7b-4272-8e49-381f0109e261",
                    "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
                    "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "invitee_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "role": "ADMIN",
                    "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "active_from": 1755518217882,
                    "expires_at": -1,
                    "created_at": 1755518217882,
                    "last_modified_at": 1755518217882,
                    "from_placeholder_invitee": null,
                    "labels": [],
                    "redeem_code": null,
                    "external_id": null,
                    "external_payload": null,
                    "group_name": "my  group",
                    "group_avatar": "",
                    "invitee_name": "Owner",
                    "invitee_avatar": null,
                    "permission_previews": [
                        "CREATE",
                        "VIEW",
                        "EDIT",
                        "DELETE",
                        "INVITE"
                    ]
                },
                {
                    "id": "GroupInviteID_c5ee7a87-6e7b-4aa6-b409-2f4af306cba2",
                    "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
                    "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "invitee_id": "PlaceholderGroupInviteeID_24a034e6-aa0e-47a4-97de-c1d8eac26f69",
                    "role": "MEMBER",
                    "note": "",
                    "active_from": 1755518224140,
                    "expires_at": -1,
                    "created_at": 1755518224637,
                    "last_modified_at": 1755518224637,
                    "from_placeholder_invitee": null,
                    "labels": [],
                    "redeem_code": "REDEEM_1755518224637",
                    "external_id": null,
                    "external_payload": null,
                    "group_name": "my  group",
                    "group_avatar": "",
                    "invitee_name": "Awaiting Anon",
                    "permission_previews": [
                        "CREATE",
                        "VIEW",
                        "EDIT",
                        "DELETE",
                        "INVITE"
                    ]
                }
            ],
            "page_size": 50,
            "total": 2,
            "direction": "ASC",
            "cursor": null
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

|          | type                                                                                                                                     |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestListGroupInvites](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1106)  |
| Response | [IResponseListGroupInvites](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1112) |

***

## Create Group Invite

Create a new group invite

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/0h55rph/drive-org-id-groups-invites-create-known?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| group\_id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupID)</strong></p><p>Unique identifier for a group</p>                                                                         | GroupID\_b810a4d0-55bb-4bbb-84cf-b044e702a10d                           |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| invitee\_id                                          | <p><strong>string (UserID)</strong></p><p>Unique identifier for a user</p>                                                                           | UserID\_ttko6-fa7zz-btluu-e7wxr-nx7we-schz3-ygt3h-3kqad-3z767-wjogx-iqe |
| role <mark style="color:red;">(required)</mark>      | <p><strong>string</strong></p><p>Enum: "<strong>ADMIN</strong>","<strong>MEMBER</strong>"</p><p>Role to assign to the invited user</p>               | MEMBER                                                                  |
| active\_from                                         | <p><strong>integer or null &#x3C;int64></strong></p><p>Timestamp when the invite becomes active</p>                                                  |                                                                         |
| expires\_at                                          | <p><strong>integer or null &#x3C;int64></strong></p><p>Timestamp when the invite expires</p>                                                         | 1672531200000                                                           |
| note                                                 | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Note about the invite</p>                                                              | Invitation to join the project group                                    |
| external\_id                                         | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                | ext-invite-001                                                          |
| external\_payload                                    | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | {"department": "engineering", "project": "alpha"}                       |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupInviteID_0ce8f7de-3ea2-470d-84e5-fbe72c7e480b",
            "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
            "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "invitee_id": "UserID_ttko6-fa7zz-btluu-e7wxr-nx7we-schz3-ygt3h-3kqad-3z767-wjogx-iqe",
            "role": "MEMBER",
            "note": "Invitation to join the project group",
            "active_from": 0,
            "expires_at": 1672531200000,
            "created_at": 1755519868849,
            "last_modified_at": 1755519868849,
            "labels": [],
            "external_id": "ext-invite-001",
            "external_payload": "{\"department\": \"engineering\", \"project\": \"alpha\"}",
            "group_name": "my  group",
            "group_avatar": "",
            "invitee_name": "Unknown User (UserID_ttko6-fa7zz-btluu-e7wxr-nx7we-schz3-ygt3h-3kqad-3z767-wjogx-iqe)",
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

|          | type                                                                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCreateGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1116)  |
| Response | [IResponseCreateGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1137) |

***

## Update Group Invite

Update group invite

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/3vdqkxe/drive-org-id-groups-invites-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupInviteID)</strong></p><p>Unique identifier for a group invite</p>                                                            | GroupInviteID\_0ce8f7de-3ea2-470d-84e5-fbe72c7e480b   |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| role                                          | <p><strong>string or null</strong><br>Enum:</p><p>"<strong>ADMIN</strong>","<strong>MEMBER</strong>"<br>New role to assign</p>                       | ADMIN                                                 |
| active\_from                                  | <p><strong>integer or null &#x3C;int64></strong></p><p>New timestamp when the invite becomes active</p>                                              |                                                       |
| expires\_at                                   | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the contact</p>                                                   | 1672531200000                                         |
| note                                          | <p><strong>string or null &#x3C;= 8192 characters</strong><br>New note about the invite</p>                                                          | Invitation to join the project group updated as admin |
| external\_id                                  | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                | ext-invite-001                                        |
| external\_payload                             | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | {"department": "engineering", "project": "alpha"}     |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupInviteID_0ce8f7de-3ea2-470d-84e5-fbe72c7e480b",
            "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
            "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "invitee_id": "UserID_ttko6-fa7zz-btluu-e7wxr-nx7we-schz3-ygt3h-3kqad-3z767-wjogx-iqe",
            "role": "ADMIN",
            "note": "Invitation to join the project group updated as admin",
            "active_from": 0,
            "expires_at": 1672531200000,
            "created_at": 1755519868849,
            "last_modified_at": 1755520730404,
            "redeem_code": null,
            "from_placeholder_invitee": null,
            "labels": [],
            "external_id": "ext-invite-001",
            "external_payload": "{\"department\": \"engineering\", \"project\": \"alpha\"}",
            "group_name": "my  group",
            "group_avatar": "",
            "invitee_name": "Unknown User (UserID_ttko6-fa7zz-btluu-e7wxr-nx7we-schz3-ygt3h-3kqad-3z767-wjogx-iqe)",
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

|          | type                                                                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestUpdateGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1141)  |
| Response | [IResponseUpdateGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1159) |

***

## Delete Group Invite

Delete an existing group invite

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/njfejhm/drive-org-id-groups-invites-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupInviteID)</strong><br>Unique identifier for a group invite</p> | GroupInviteID\_0ce8f7de-3ea2-470d-84e5-fbe72c7e480b |
| --------------------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupInviteID_0ce8f7de-3ea2-470d-84e5-fbe72c7e480b",
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

|          | type                                                                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDeleteGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1163)  |
| Response | [IResponseDeleteGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1169) |

***

## Redeem Group Invite

Redeem a group invite for a specific user

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/invites/redeem
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

| invite\_id <mark style="color:red;">(required)</mark>   | <p><strong>string (GroupInviteID)</strong><br>Unique identifier for a group invite</p>    | GroupInviteID\_c5ee7a87-6e7b-4aa6-b409-2f4af306cba2 |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------- |
| redeem\_code <mark style="color:red;">(required)</mark> | <p><strong>string</strong><br>redeem code for the Invite</p>                              | REDEEM\_1755518224637                               |
| note                                                    | <p><strong>string &#x3C;= 512 characters</strong><br>Optional note for the redemption</p> |                                                     |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "invite": {
                "id": "GroupInviteID_c5ee7a87-6e7b-4aa6-b409-2f4af306cba2",
                "group_id": "GroupID_b810a4d0-55bb-4bbb-84cf-b044e702a10d",
                "inviter_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                "invitee_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                "role": "MEMBER",
                "note": "Note from User: Redeemed by \"Anon\" on 7/23/2025, 11:07:42 PM, Prior Original Note: ",
                "active_from": 1755518224140,
                "expires_at": -1,
                "created_at": 1755518224637,
                "last_modified_at": 1755522442480,
                "redeem_code": null,
                "from_placeholder_invitee": "PlaceholderGroupInviteeID_24a034e6-aa0e-47a4-97de-c1d8eac26f69",
                "labels": [],
                "external_id": null,
                "external_payload": null
            }
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

|          | type                                                                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestRedeemGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1178)  |
| Response | [IResponseRedeemGroupInvite](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1186) |
