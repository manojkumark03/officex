---
description: Operations for managing directory and system permissions
---

# Permissions by Directory

## Get Directory Permission

Retrieve a directory permission by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/get/{directory_permission_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/tgmx2qu/drive-org-id-disks-get-disk-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark>          | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>            | DriveID\_abc123                                             |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| directory\_permission\_id <mark style="color:red;">(required)</mark> | <p></p><p><strong>string</strong> </p><p>ID of the directory permission to retrieve</p> | DirectoryPermissionID\_3acdba66-1378-4257-bc9b-0563dd9c3bbf |

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
            "id": "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf",
            "resource_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
            "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::",
            "granted_to": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
            "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "permission_types": [
                "DELETE",
                "EDIT",
                "INVITE",
                "MANAGE",
                "UPLOAD",
                "VIEW"
            ],
            "begin_date_ms": 0,
            "expiry_date_ms": -1,
            "inheritable": true,
            "note": "Default permissions for disk root folder owner",
            "created_at": 1755588857475,
            "last_modified_at": 1755588857475,
            "from_placeholder_grantee": null,
            "labels": [],
            "redeem_code": null,
            "resource_name": "",
            "grantee_name": "Group for All",
            "grantee_avatar": null,
            "granter_name": "Owner",
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestGetDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L700)  |
| Response | [IResponseGetDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L706) |

***

## Create Directory Permission

Create a new directory permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/20l4mlg/drive-org-id-permissions-directory-create-permit-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| resource\_id <mark style="color:red;">(required)</mark>      | <p><strong>string(DirectoryResourceID)</strong></p><p>Enum: "<strong>FileID_&#x3C;id></strong>" "<strong>FolderID_&#x3C;id></strong>"</p><p>Unique identifier for a directory resource (file or folder)</p> | FolderID\_b9fa11bc-2926-4a13-944e-e1189df66e5a                            |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| granted\_to                                                  | <p><strong>string (GranteeID)</strong><br>Either a UserID or GroupID</p>                                                                                                                                    |                                                                           |
| permission\_types <mark style="color:red;">(required)</mark> | **Array of permissions**                                                                                                                                                                                    | <p>[<br>"VIEW",<br>"EDIT",<br>"DELETE",<br>"UPLOAD",<br>"INVITE"<br>]</p> |
| begin\_date\_ms                                              | **number**                                                                                                                                                                                                  |                                                                           |
| expiry\_date\_ms                                             | **number**                                                                                                                                                                                                  |                                                                           |
| inheritable                                                  | <p><strong>boolean</strong><br>Whether permission applies to sub-resources</p>                                                                                                                              | false                                                                     |
| note                                                         | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Note about the permission</p>                                                                                                                 |                                                                           |
| metadata                                                     | <p><strong>object or null</strong><br>Additional metadata for the permission</p>                                                                                                                            |                                                                           |
| external\_id                                                 | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong><br>External identifier for integration purposes</p>                                                                                          |                                                                           |
| external\_payload                                            | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong><br>Additional data for external integrations. Eg Stringified JSON</p>                                                                  |                                                                           |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "permission": {
                "id": "DirectoryPermissionID_bddd1bb7-f292-448a-a9dc-6a82bb88627f",
                "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::../",
                "granted_to": "PlaceholderPermissionGranteeID_2831cde1-1312-4630-b2a8-c371fd57ee35",
                "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "permission_types": [
                    "DELETE",
                    "EDIT",
                    "INVITE",
                    "UPLOAD",
                    "VIEW"
                ],
                "begin_date_ms": 0,
                "expiry_date_ms": -1,
                "inheritable": false,
                "note": "",
                "created_at": 1755612642222,
                "last_modified_at": 1755612642222,
                "from_placeholder_grantee": null,
                "labels": [],
                "redeem_code": "RedeemTokenID_8b4b9786-60bb-494c-b0a6-b9e66ed06e79",
                "resource_name": "Revised Investigation (2) (2)",
                "grantee_name": "Awaiting Anon",
                "granter_name": "Owner",
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

|          | type                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestCreateDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L738)  |
| Response | [IResponseCreateDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L764) |

***

## Update Directory Permission

Update directory permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/b6ekres/drive-org-id-permissions-directory-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark>                | <p><strong>string (DirectoryPermissionID)</strong><br>Unique identifier for a directory permission</p>                                     | DirectoryPermissionID\_bddd1bb7-f292-448a-a9dc-6a82bb88627f |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- |
| permission\_types <mark style="color:red;">(required)</mark> | **Array of permissions**                                                                                                                   | <p>[<br>"DELETE"<br>]</p>                                   |
| begin\_date\_ms                                              | **number**                                                                                                                                 |                                                             |
| expiry\_date\_ms                                             | **number**                                                                                                                                 |                                                             |
| inheritable                                                  | <p><strong>boolean</strong><br>Whether permission applies to sub-resources</p>                                                             | false                                                       |
| note                                                         | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Note about the permission</p>                                                |                                                             |
| metadata                                                     | <p><strong>object or null</strong><br>Additional metadata for the permission</p>                                                           |                                                             |
| external\_id                                                 | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong><br>External identifier for integration purposes</p>                         |                                                             |
| external\_payload                                            | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong><br>Additional data for external integrations. Eg Stringified JSON</p> |                                                             |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "permission": {
                "id": "DirectoryPermissionID_bddd1bb7-f292-448a-a9dc-6a82bb88627f",
                "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::../",
                "granted_to": "PlaceholderPermissionGranteeID_2831cde1-1312-4630-b2a8-c371fd57ee35",
                "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "permission_types": [
                    "DELETE"
                ],
                "begin_date_ms": 0,
                "expiry_date_ms": -1,
                "inheritable": false,
                "note": "",
                "created_at": 1755612642222,
                "last_modified_at": 1755612642222,
                "from_placeholder_grantee": null,
                "labels": [],
                "redeem_code": "RedeemTokenID_8b4b9786-60bb-494c-b0a6-b9e66ed06e79",
                "resource_name": "Revised Investigation (2) (2)",
                "grantee_name": "Awaiting Anon",
                "granter_name": "Owner",
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

|          | type                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestUpdateDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L768)  |
| Response | [IResponseUpdateDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L790) |

***

## Delete Directory Permission

Delete an existing directory permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/u88a1xm/drive-org-id-permissions-directory-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| permission\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DirectoryPermissionID)</strong><br>Unique identifier for a directory permission</p> | DirectoryPermissionID\_bddd1bb7-f292-448a-a9dc-6a82bb88627f |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "deleted_id": "DirectoryPermissionID_bddd1bb7-f292-448a-a9dc-6a82bb88627f"
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

|          | type                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestDeleteDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L794)  |
| Response | [IResponseDeleteDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L800) |

***

## Check Permissions by Directory&#x20;

Check what permissions a user has for a specific resource

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/check
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/tdb42bz/drive-org-id-permissions-directory-check?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| resource\_id <mark style="color:red;">(required)</mark> | **string (DirectoryResourceID)** Enum: "FileID\_" "FolderID\_" Unique identifier for a directory resource (file or folder) | FolderID\_b9fa11bc-2926-4a13-944e-e1189df66e5a                          |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| grantee\_id <mark style="color:red;">(required)</mark>  | <p><strong>string (GranteeID)</strong><br>Either a UserID or GroupID</p>                                                   | UserID\_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
            "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
            "permissions": [
                "DELETE",
                "EDIT",
                "INVITE",
                "UPLOAD",
                "VIEW"
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

|          | type                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestCheckDirectoryPermissions](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L807)  |
| Response | [IResponseCheckDirectoryPermissions](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L815) |

***

## Redeem Directory Permission

Redeem a placeholder permission for a specific user

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/directory/redeem
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/y4o1576/drive-org-id-permissions-directory-redeem?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| permission\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DirectoryPermissionID)</strong></p><p>Unique identifier for a directory permission</p> | DirectoryPermissionID\_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37             |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| user\_id <mark style="color:red;">(required)</mark>       | <p><strong>string (UserID)</strong><br>Unique identifier for a user</p>                                   | UserID\_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe |
| redeem\_code <mark style="color:red;">(required)</mark>   | <p><strong>string</strong><br>Optional redeem code for the permission</p>                                 | RedeemTokenID\_8e82fb3c-7c7d-4aec-8329-935d27747b44                     |
| note                                                      | <p><strong>string</strong><br>Optional note for the redemption</p>                                        | Hello World                                                             |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "permission": {
                "id": "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739",
                "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::../",
                "granted_to": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "permission_types": [
                    "DELETE",
                    "EDIT",
                    "INVITE",
                    "UPLOAD",
                    "VIEW"
                ],
                "begin_date_ms": 0,
                "expiry_date_ms": -1,
                "inheritable": false,
                "note": "Hello World",
                "created_at": 1755614678534,
                "last_modified_at": 1755614702963,
                "from_placeholder_grantee": "PlaceholderPermissionGranteeID_7c7c2517-c7f7-4ae9-8448-701bc5feaedd",
                "labels": [],
                "redeem_code": null,
                "resource_name": "Revised Investigation (2) (2)",
                "grantee_name": "Unknown User (UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe)",
                "granter_name": "Owner",
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

|          | type                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestRedeemDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L826)  |
| Response | [IResponseRedeemDirectoryPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L836) |
