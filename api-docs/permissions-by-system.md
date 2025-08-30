---
description: Operations for managing directory and system permissions
---

# Permissions by System

## Get System Permission

Retrieve a system permission by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/get/{system_permission_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/s2je3pg/drive-org-id-permissions-system-get-systempermissionid?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark>       | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>     | DriveID\_abc123                                             |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| system\_permission\_id <mark style="color:red;">(required)</mark> | <p></p><p><strong>string</strong><br>ID of the system permission to retrieve</p> | DirectoryPermissionID\_3acdba66-1378-4257-bc9b-0563dd9c3bbf |

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

## Create System Permission&#x20;

Create a new system permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ujglv6d/drive-org-id-permissions-system-create?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| resource\_id <mark style="color:red;">(required)</mark>      | <p><strong>SystemTableResource (object) or SystemRecordResource (object) (SystemResourceID)</strong></p><p>Unique identifier for a system resource (table or record)</p>                     | TABLE\_CONTACTS                                                         |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| granted\_to                                                  | <p><strong>string (GranteeID)</strong><br>Either a UserID or GroupID</p>                                                                                                                     | UserID\_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe |
| permission\_types <mark style="color:red;">(required)</mark> | <p><strong>Array of permissions</strong></p><p>Items Enum: "<strong>CREATE</strong>" "<strong>EDIT</strong>" "<strong>DELETE</strong>" "<strong>VIEW</strong>" "<strong>INVITE</strong>"</p> | <p>[<br>"VIEW",<br>"CREATE",<br>]</p>                                   |
| begin\_date\_ms                                              | **number**                                                                                                                                                                                   | 1753290541568                                                           |
| expiry\_date\_ms                                             | **number**                                                                                                                                                                                   | -1                                                                      |
| inheritable                                                  | <p><strong>boolean</strong><br>Whether permission applies to sub-resources</p>                                                                                                               |                                                                         |
| note                                                         | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Note about the permission</p>                                                                                                  |                                                                         |
| metadata                                                     | <p><strong>object or null</strong><br>Additional metadata for the permission</p>                                                                                                             |                                                                         |
| external\_id                                                 | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong><br>External identifier for integration purposes</p>                                                                           |                                                                         |
| external\_payload                                            | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong><br>Additional data for external integrations. Eg Stringified JSON</p>                                                   |                                                                         |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "permission": {
                "id": "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
                "resource_id": "TABLE_CONTACTS",
                "granted_to": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "permission_types": [
                    "CREATE",
                    "VIEW"
                ],
                "begin_date_ms": 1753290541568,
                "expiry_date_ms": -1,
                "note": "",
                "created_at": 1755655944656,
                "last_modified_at": 1755655944656,
                "from_placeholder_grantee": null,
                "labels": [],
                "redeem_code": null,
                "resource_name": "TABLE_CONTACTS",
                "grantee_name": "User: UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                "grantee_avatar": "",
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCreateSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L889)  |
| Response | [IResponseCreateSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L912) |

***

## Update System Permission

Update system permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/cdpg94m/drive-org-id-permissions-system-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (DirectoryPermissionID)</strong><br>Unique identifier for a directory permission</p>                                     | SystemPermissionID\_8743dd9e-7f1a-457a-8560-b3c995da7591 |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| resource\_id                                  | <p><strong>string</strong></p><p>ID of the user/group to grant permission to</p>                                                           |                                                          |
| granted\_to                                   | <p><strong>string (GranteeID)</strong><br>Either a UserID or GroupID</p>                                                                   |                                                          |
| permission\_types                             | **Array of permissions**                                                                                                                   | <p>[<br>"CREATE",<br>"VIEW",<br>"EDIT"<br>]</p>          |
| begin\_date\_ms                               | **number**                                                                                                                                 | 1753290541568                                            |
| expiry\_date\_ms                              | **number**                                                                                                                                 | 0                                                        |
| inheritable                                   | <p><strong>boolean</strong><br>Whether permission applies to sub-resources</p>                                                             |                                                          |
| note                                          | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Note about the permission</p>                                                |                                                          |
| metadata                                      | <p><strong>object or null</strong><br>Additional metadata for the permission</p>                                                           |                                                          |
| external\_id                                  | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong><br>External identifier for integration purposes</p>                         |                                                          |
| external\_payload                             | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong><br>Additional data for external integrations. Eg Stringified JSON</p> |                                                          |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
            "resource_id": "TABLE_CONTACTS",
            "granted_to": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
            "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "permission_types": [
                "CREATE",
                "EDIT",
                "VIEW"
            ],
            "begin_date_ms": 1753290541568,
            "expiry_date_ms": 0,
            "note": "",
            "created_at": 1755655944656,
            "last_modified_at": 1755656836765,
            "from_placeholder_grantee": null,
            "labels": [],
            "redeem_code": null,
            "resource_name": "TABLE_CONTACTS",
            "grantee_name": "User: UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
            "grantee_avatar": "",
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestUpdateSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L916)  |
| Response | [IResponseUpdateSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L940) |

***

## Delete System Permission

Delete an existing system permission

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ebu38r7/drive-org-id-permissions-system-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| permission\_id <mark style="color:red;">(required)</mark> | <p><strong>string (SystemPermissionID)</strong><br>Unique identifier for a system permission</p> | SystemPermissionID\_0298d45b-561a-4abe-8f16-2255cca5896a |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "deleted_id": "SystemPermissionID_0298d45b-561a-4abe-8f16-2255cca5896a"
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDeleteSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L944)  |
| Response | [IResponseDeleteSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L950) |

***

## Check Permissions by System (PENDING)

Check what permissions a user has for a specific system resource

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/check
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/4b9pmmz/drive-org-id-permissions-system-check?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| resource\_id <mark style="color:red;">(required)</mark> | <p><strong>SystemTableResource (object) or SystemRecordResource (object) (SystemResourceID)</strong><br>Unique identifier for a system resource (table or record)</p> | TABLE\_CONTACTS                                                         |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| grantee\_id <mark style="color:red;">(required)</mark>  | <p><strong>string (GranteeID)</strong><br>Either a UserID or GroupID</p>                                                                                              | UserID\_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "resource_id": "TABLE_CONTACTS",
            "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
            "permissions": [
                "CREATE",
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCheckSystemPermissions](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L957)  |
| Response | [IResponseCheckSystemPermissions](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L965) |

***

## Redeem System Permission

Redeem a placeholder permission for a specific user

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/permissions/system/redeem
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/7kruuq6/drive-org-id-permissions-system-redeem?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| permission\_id <mark style="color:red;">(required)</mark> | <p><strong>string (SystemPermissionID)</strong></p><p>Unique identifier for a system permission</p> | SystemPermissionID\_0298d45b-561a-4abe-8f16-2255cca5896a                |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| user\_id <mark style="color:red;">(required)</mark>       | <p><strong>string (UserID)</strong><br>Unique identifier for a user</p>                             | UserID\_dfyb3-s744h-ld6eq-dgrdk-behew-vcdto-kqacs-htufx-u7a4j-clpdf-5qe |
| redeem\_code <mark style="color:red;">(required)</mark>   | <p><strong>string</strong><br>Optional redeem code for the permission</p>                           | REDEEM\_1755657620659000                                                |
| note                                                      | <p><strong>string</strong><br>Optional note for the redemption</p>                                  |                                                                         |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "SystemPermissionID_0298d45b-561a-4abe-8f16-2255cca5896a",
            "resource_id": "TABLE_CONTACTS",
            "granted_to": "UserID_dfyb3-s744h-ld6eq-dgrdk-behew-vcdto-kqacs-htufx-u7a4j-clpdf-5qe",
            "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "permission_types": [
                "CREATE",
                "VIEW"
            ],
            "begin_date_ms": 1753290541568,
            "expiry_date_ms": -1,
            "note": "",
            "created_at": 1755657620659,
            "last_modified_at": 1755657681427,
            "from_placeholder_grantee": "PlaceholderPermissionGranteeID_0f4bd9a3-08db-4740-8626-2a417bfe0a34",
            "labels": [],
            "redeem_code": null,
            "resource_name": "TABLE_CONTACTS",
            "grantee_name": "User: UserID_dfyb3-s744h-ld6eq-dgrdk-behew-vcdto-kqacs-htufx-u7a4j-clpdf-5qe",
            "grantee_avatar": "",
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

|          | type                                                                                                                                          |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestRedeemSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L976)  |
| Response | [IResponseRedeemSystemPermission](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L986) |
