---
description: Operations for managing disks
---

# Disks

## Get Disk

Retrieve a disk by its ID

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/disks/get/{disk_id}
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/tgmx2qu/drive-org-id-disks-get-disk-id?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p>     | DriveID\_abc123                              |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------- |
| disk\_id <mark style="color:red;">(required)</mark>         | <p></p><p><strong>string (DiskID)</strong> </p><p>ID of the Disk to retrieve</p> | DiskID\_3574c5fd-9dea-4934-9dbc-f3ddb5bff1e5 |

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
            "id": "DiskID_3574c5fd-9dea-4934-9dbc-f3ddb5bff1e5",
            "name": "new disk",
            "disk_type": "LOCAL_SSD",
            "private_note": null,
            "public_note": null,
            "auth_json": null,
            "created_at": 1755524581236,
            "root_folder": "FolderID_8ca1bbbe-297a-4e97-a5ea-c4699ad32e4f",
            "trash_folder": "FolderID_e082ed3b-c43a-4986-94bd-9883cb280182",
            "external_id": null,
            "external_payload": null,
            "endpoint": null,
            "autoexpire_ms": null,
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ],
            "labels": []
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

|          | type                                                                                                                          |
| -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestGetDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L441) |
| Response | [IRequestGetDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L447) |

***

## List Disks

List disks with optional filtering and pagination

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/disks/list
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/scphc6t/drive-org-id-disks-list?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| <p><br>filters </p> | <p><strong>string &#x3C;= 256 characters</strong><br>Default: ""<br>Filter string for disks</p>        |        |
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
                    "id": "DiskID_3574c5fd-9dea-4934-9dbc-f3ddb5bff1e5",
                    "name": "new disk",
                    "disk_type": "LOCAL_SSD",
                    "private_note": null,
                    "public_note": null,
                    "auth_json": null,
                    "created_at": 1755524581236,
                    "root_folder": "FolderID_8ca1bbbe-297a-4e97-a5ea-c4699ad32e4f",
                    "trash_folder": "FolderID_e082ed3b-c43a-4986-94bd-9883cb280182",
                    "external_id": null,
                    "external_payload": null,
                    "endpoint": null,
                    "autoexpire_ms": null,
                    "labels": [],
                    "permission_previews": [
                        "CREATE",
                        "VIEW",
                        "EDIT",
                        "DELETE",
                        "INVITE"
                    ]
                }
            ],
            "page_size": 1,
            "total": 1,
            "direction": "ASC"
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
| Request  | [IRequestListDisks](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L450)  |
| Response | [IResponseListDisks](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L453) |

***

## Create Disk

Create a new Disk

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/disks/create
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/shtei58/drive-org-id-disks-create?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| name <mark style="color:red;">(required)</mark>       | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the disk</p>                                                                                                                                                                           | Project Cloud Storage                                                                                                                    |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| disk\_type <mark style="color:red;">(required)</mark> | <p><strong>string (DiskType)</strong><br>Enum: "<strong>BrowserCache</strong>","<strong>LocalSSD</strong>" ,"<strong>AwsBucket</strong>" ,"<strong>StorjWeb3</strong>", "<strong>IcpCanister</strong>"<br>Type of disk storage, currently supported</p> | AWS\_BUCKET                                                                                                                              |
| public\_note                                          | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the disk</p>                                                                                                                                                         | Storage for group project files                                                                                                          |
| private\_note                                         | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the disk</p>                                                                                                                                                        | Contains sensitive project data                                                                                                          |
| auth\_json                                            | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Authentication JSON for the disk</p>                                                                                                                                                      | {"access\_key": "redacted", "secret\_key": "redacted", "region": "us-east-1", "bucket": "ofx-bucket-friend-696", "endpoint": "redacted"} |
| external\_id                                          | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                                                                                                                   | ext-disk-001                                                                                                                             |
| external\_payload                                     | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p>                                                                                                    | {"department": "engineering", "cost\_center": "cc-12345", "project\_id": "p-987654"}                                                     |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "DiskID_6320bd41-f966-4052-a067-a9f33d6dfe39",
            "name": "Project Cloud Storage",
            "disk_type": "AWS_BUCKET",
            "private_note": "Contains sensitive project data",
            "public_note": "Storage for group project files",
            "auth_json": "{\"access_key\": \"redacted\", \"secret_key\": \"redacted\", \"region\": \"us-east-1\", \"bucket\": \"ofx-bucket-friend-696\", \"endpoint\": \"redacted\"}",
            "labels": [],
            "created_at": 1755525705285,
            "root_folder": "FolderID_c9107c9a-4f1f-444f-b921-1ebce17cfbf1",
            "trash_folder": "FolderID_8110dace-1e6e-4224-93f0-47c787c7e11d",
            "external_id": "ext-disk-001",
            "external_payload": "{\"department\": \"engineering\", \"cost_center\": \"cc-12345\", \"project_id\": \"p-987654\"}",
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

|          | type                                                                                                                              |
| -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestCreateDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L457)  |
| Response | [IResponseCreateDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L477) |

***

## Update Disk

Update a disk

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/disks/update
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/3hu9p6u/drive-org-id-disks-update?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark>   | <p><strong>string (DiskID)</strong><br>Unique identifier for a disk</p>                                                                              | DiskID\_6320bd41-f966-4052-a067-a9f33d6dfe39                                                                                         |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| name <mark style="color:red;">(required)</mark> | <p><strong>string &#x3C;= 256 characters</strong></p><p>Name for the disk</p>                                                                        | Updated Storage Name                                                                                                                 |
| public\_note                                    | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Public note about the disk</p>                                                      | Primary storage for project Alpha                                                                                                    |
| private\_note                                   | <p><strong>string or null &#x3C;= 8192 characters</strong></p><p>Private note about the disk</p>                                                     | Contains confidential project data                                                                                                   |
| auth\_json                                      | <p><strong>string or null &#x3C;= 8192 characters</strong><br>Authentication JSON for the disk</p>                                                   | {"endpoint": "redacted","access\_key": "redacted","secret\_key": "redacted", "region": "us-east-1", "bucket": "project-alpha-files"} |
| external\_id                                    | <p><strong>string (ExternalID) &#x3C;= 256 characters</strong></p><p>External identifier for integration purposes</p>                                | ext-disk-001-updated                                                                                                                 |
| external\_payload                               | <p><strong>string (ExternalPayload) &#x3C;= 8192 characters</strong></p><p>Additional data for external integrations. </p><p>Eg Stringified JSON</p> | {"department": "engineering", "cost\_center": "cc-67890", "project\_id": "p-123456", "updated": true}                                |

</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "DiskID_6320bd41-f966-4052-a067-a9f33d6dfe39",
            "name": "Updated Storage Name",
            "disk_type": "AWS_BUCKET",
            "private_note": "Contains confidential project data",
            "public_note": "Primary storage for project Alpha",
            "auth_json": "{\"endpoint\": \"redacted\",\"access_key\": \"redacted\",\"secret_key\": \"redacted\", \"region\": \"us-east-1\", \"bucket\": \"project-alpha-files\"}",
            "created_at": 1755525705285,
            "root_folder": "FolderID_c9107c9a-4f1f-444f-b921-1ebce17cfbf1",
            "trash_folder": "FolderID_8110dace-1e6e-4224-93f0-47c787c7e11d",
            "external_id": "ext-disk-001-updated",
            "external_payload": "{\"department\": \"engineering\", \"cost_center\": \"cc-67890\", \"project_id\": \"p-123456\", \"updated\": true}",
            "endpoint": null,
            "autoexpire_ms": null,
            "permission_previews": [
                "CREATE",
                "VIEW",
                "EDIT",
                "DELETE",
                "INVITE"
            ],
            "labels": []
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

|          | type                                                                                                                              |
| -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestUpdateDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L480)  |
| Response | [IResponseUpdateDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L499) |

***

## Delete Disk

Delete an existing disk

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/disks/delete
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/5h1xmph/drive-org-id-disks-delete?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| id <mark style="color:red;">(required)</mark> | <p><strong>string (DiskID)</strong><br>Unique identifier for a disk</p> | DiskID\_6320bd41-f966-4052-a067-a9f33d6dfe39 |
| --------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "id": "DiskID_6320bd41-f966-4052-a067-a9f33d6dfe39",
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

|          | type                                                                                                                              |
| -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDeleteDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L502)  |
| Response | [IResponseDeleteDisk](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L508) |

***
