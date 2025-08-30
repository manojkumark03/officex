---
description: Operations for managing groups
---

# Groups

## Get Group

Retrieve a group by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/get/{group_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/f97uccq/drive-org-id-groups-get-group-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>       | DriveID\_abc123                      |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------ |
| group\_id <mark style="color:red;">(required)</mark>        | <p></p><p><strong>string (GroupID)</strong> </p><p>ID of the group to retrieve</p> | GroupID\_c18e812c-ff0b-4dd9-a28c-... |

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
            "id": "GroupID_c18e812c-ff0b-4dd9-a28c-4b650565bb0d",
            "name": "group monsters",
            "owner": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "avatar": "",
            "private_note": "",
            "public_note": "",
            "admin_invites": [
                "GroupInviteID_81be383f-e440-4915-ade2-cbe73d626e4e"
            ],
            "member_invites": [
                "GroupInviteID_81be383f-e440-4915-ade2-cbe73d626e4e"
            ],
            "created_at": 1755494291625,
            "last_modified_at": 1755494291625,
            "drive_id": "DriveID_y6ekb-v2qhu-f5mnu-iukkc-qybbs-urd75-76sdu-4h6xc-5ewg4-kd76c-wae",
            "host_url": "https://officex.otterpad.cc",
            "labels": [],
            "external_id": null,
            "external_payload": null,
            "member_previews": [
                {
                    "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "name": "Owner",
                    "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "group_id": "GroupID_c18e812c-ff0b-4dd9-a28c-4b650565bb0d",
                    "is_admin": true,
                    "invite_id": "GroupInviteID_81be383f-e440-4915-ade2-cbe73d626e4e",
                    "last_online_ms": 1755494351053
                }
            ],
            "permission_previews": [
                "CREATE",
                "EDIT",
                "DELETE",
                "INVITE",
                "VIEW"
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
| Request  | [IRequestGetGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L997)   |
| Response | [IResponseGetGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1003) |

***

## List Groups

List groups with optional filtering and pagination

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/list
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/fh9whdm/drive-org-id-groups-list?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| <p><br>filters </p> | <p><strong>string &#x3C;= 256 characters</strong><br>Default: ""<br>Filter string for groups</p>       |        |
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
    "ok": {
        "data": {
            "items": [
                {
                    "id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                    "name": "Group for All",
                    "owner": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "avatar": null,
                    "public_note": null,
                    "private_note": null,
                    "created_at": 1755438223829,
                    "last_modified_at": 1755438223829,
                    "drive_id": "DriveID_y6ekb-v2qhu-f5mnu-iukkc-qybbs-urd75-76sdu-4h6xc-5ewg4-kd76c-wae",
                    "host_url": "https://officex.otterpad.cc",
                    "external_id": null,
                    "external_payload": null,
                    "member_previews": [
                        {
                            "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                            "name": "Owner",
                            "note": "giftcard GiftcardSpawnOrgID_f7c7045d-fbc7-4111-9893-c4f7c0daca61 was redeemed to spawn drive with 3500000000000 cycles, owned by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae, on timestamp_ms 1755438223829 2025-08-17T13:43:43.829Z",
                            "group_id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                            "is_admin": true,
                            "invite_id": "GroupInviteID_6f72886f-477a-40c0-aa5b-d5f208267fcd",
                            "last_online_ms": 1755494922756
                        },
                        {
                            "user_id": "UserID_c5hjz-wpnfl-3v2jx-hglmv-6y7wm-o6zur-e6q2n-e7vp3-4z762-ajc7l-mqe",
                            "name": "manzy",
                            "note": "Auto-invited to default 'Group for All' upon contact creation.",
                            "group_id": "GroupID_b76e4405-d850-4685-88b8-c66744255724",
                            "is_admin": false,
                            "invite_id": "GroupInviteID_e8479d67-0806-4ee3-bb75-6ff5245ee21e",
                            "last_online_ms": 0
                        }
                    ],
                    "permission_previews": [
                        "CREATE",
                        "VIEW",
                        "EDIT",
                        "DELETE",
                        "INVITE"
                    ]
                },
                {
                    "id": "GroupID_c18e812c-ff0b-4dd9-a28c-4b650565bb0d",
                    "name": "group monsters",
                    "owner": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "avatar": "",
                    "public_note": "",
                    "private_note": "",
                    "created_at": 1755494291625,
                    "last_modified_at": 1755494291625,
                    "drive_id": "DriveID_y6ekb-v2qhu-f5mnu-iukkc-qybbs-urd75-76sdu-4h6xc-5ewg4-kd76c-wae",
                    "host_url": "https://officex.otterpad.cc",
                    "external_id": null,
                    "external_payload": null,
                    "member_previews": [
                        {
                            "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                            "name": "Owner",
                            "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                            "group_id": "GroupID_c18e812c-ff0b-4dd9-a28c-4b650565bb0d",
                            "is_admin": true,
                            "invite_id": "GroupInviteID_81be383f-e440-4915-ade2-cbe73d626e4e",
                            "last_online_ms": 1755494922756
                        }
                    ],
                    "permission_previews": [
                        "CREATE",
                        "VIEW",
                        "EDIT",
                        "DELETE",
                        "INVITE"
                    ]
                }
            ],
            "page_size": 2,
            "total": 2,
            "direction": "ASC",
            "cursor": ""
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

|          | type                                                                                                                               |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestListGroups](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1006)  |
| Response | [IResponseListGroups](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1009) |

***

## Create Group

Create a new group

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/6vdwilu/drive-org-id-groups-create?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| name              | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the contact</p>                                                                     | Product Design Team                               |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| avatar            | <p><strong>string or null &#x3C;= 2048 characters</strong></p><p>Profile picture URL</p>                                                             |                                                   |
| public\_note      | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the contact</p>                                                   | Core product development group                    |
| private\_note     | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the contact</p>                                                  | Primary contact for urgent issues                 |
| host\_url         | <p><strong>string or null &#x3C;= 4096 characters</strong><br>URL endpoint for the group</p>                                                         |                                                   |
| external\_id      | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                |                                                   |
| external\_payload | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | {"department": "engineering", "project": "alpha"} |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupID_dfa08703-c707-495c-8ffd-996ab4c74ba9",
            "name": "Product Design Team",
            "owner": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "avatar": "",
            "public_note": "Core product development group",
            "created_at": 1755495309551,
            "last_modified_at": 1755495309551,
            "drive_id": "DriveID_y6ekb-v2qhu-f5mnu-iukkc-qybbs-urd75-76sdu-4h6xc-5ewg4-kd76c-wae",
            "host_url": "https://officex.otterpad.cc",
            "labels": [],
            "external_id": "",
            "external_payload": "{\"department\": \"engineering\", \"project\": \"alpha\"}",
            "admin_invites": [],
            "member_invites": [],
            "member_previews": [
                {
                    "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "name": "Owner",
                    "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "avatar": null,
                    "group_id": "GroupID_dfa08703-c707-495c-8ffd-996ab4c74ba9",
                    "is_admin": true,
                    "invite_id": "GroupInviteID_55251152-e7c9-4443-92f6-9c4959baae2b",
                    "last_online_ms": 1755495309539
                }
            ],
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

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCreateGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1013)  |
| Response | [IResponseCreateGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1032) |

***

## Update Group

Update group

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/h653hiy/drive-org-id-groups-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupID)</strong></p><p>Unique identifier for a group</p>                                                                         | GroupID\_dfa08703-c707-495c-8ffd-996ab4c74ba9                      |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| name                                          | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the contact</p>                                                                     | Product Design Team                                                |
| avatar                                        | <p><strong>string or null &#x3C;= 2048 characters</strong></p><p>Profile picture URL</p>                                                             |                                                                    |
| public\_note                                  | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the contact</p>                                                   | Core product development group                                     |
| private\_note                                 | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the contact</p>                                                  | Updated group structure                                            |
| host\_url                                     | <p><strong>string or null &#x3C;= 4096 characters</strong><br>URL endpoint for the group</p>                                                         |                                                                    |
| external\_id                                  | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                |                                                                    |
| external\_payload                             | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | {"department": "engineering", "project": "alpha", "updated": true} |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupID_dfa08703-c707-495c-8ffd-996ab4c74ba9",
            "name": "Product & Design",
            "owner": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
            "avatar": "",
            "private_note": "Updated group structure",
            "public_note": "Core product development group",
            "admin_invites": [
                "GroupInviteID_55251152-e7c9-4443-92f6-9c4959baae2b"
            ],
            "member_invites": [
                "GroupInviteID_55251152-e7c9-4443-92f6-9c4959baae2b"
            ],
            "created_at": 1755495309551,
            "last_modified_at": 1755495965034,
            "drive_id": "DriveID_y6ekb-v2qhu-f5mnu-iukkc-qybbs-urd75-76sdu-4h6xc-5ewg4-kd76c-wae",
            "host_url": "https://officex.otterpad.cc",
            "labels": [],
            "external_id": "",
            "external_payload": "{\"department\": \"engineering\", \"project\": \"alpha\", \"updated\": true}",
            "member_previews": [
                {
                    "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "name": "Owner",
                    "note": "Added as ADMIN by UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae",
                    "avatar": null,
                    "group_id": "GroupID_dfa08703-c707-495c-8ffd-996ab4c74ba9",
                    "is_admin": true,
                    "invite_id": "GroupInviteID_55251152-e7c9-4443-92f6-9c4959baae2b",
                    "last_online_ms": 1755495965010
                }
            ],
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

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestUpdateGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1035)  |
| Response | [IResponseUpdateGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1055) |

***

## Delete Group

Delete an existing group

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/drgx3e4/drive-org-id-groups-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupID)</strong><br>Unique identifier for a group</p> | GroupID\_dfa08703-c707-495c-8ffd-996ab4c74ba9 |
| --------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "GroupID_dfa08703-c707-495c-8ffd-996ab4c74ba9",
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

|          | type                                                                                                                                |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDeleteGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1058)  |
| Response | [IResponseDeleteGroup](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1064) |

***

## Validate Member

Verify if a user belongs to a specific group

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/groups/validate
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/gu12bos/drive-org-id-groups-validate?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| user\_id <mark style="color:red;">(required)</mark>  | <p><strong>string (GroupID)</strong><br>Unique identifier for a user</p>  | UserID\_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae |
| ---------------------------------------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| group\_id <mark style="color:red;">(required)</mark> | <p><strong>string (GroupID)</strong><br>Unique identifier for a group</p> | GroupID\_c18e812c-ff0b-4dd9-a28c-4b650565bb0d                           |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "is_member": true,
            "group_id": "GroupID_c18e812c-ff0b-4dd9-a28c-4b650565bb0d",
            "user_id": "UserID_apoe6-dkjea-p3gvd-oski2-4dgfx-phw7b-3uer5-lggpc-h3tun-vkzg4-5ae"
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

|          | type                                                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestValidateGroupMember](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1073)  |
| Response | [IResponseValidateGroupMember](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1081) |
