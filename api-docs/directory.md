---
description: Operations for managing files and folders
---

# Directory

## List Directory

List files and folders within a specified directory

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/directory/list
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/wzq2nx1/drive-org-id-directory-list-basics?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| folder\_id          | <p><strong>string or null</strong><br>ID of the folder to list contents from</p>                  | FolderID\_c9107c9a-4f1f-444f-b921-1ebce17cfbf1 |
| ------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| path                | <p><strong>string or null</strong><br>Path to the folder to list contents from</p>                |                                                |
| <p><br>filters </p> | <p><strong>string &#x3C;= 256 characters</strong><br>Default: ""<br>Filter string for disks</p>   |                                                |
| page\_size          | <p><strong>integer [ 1 .. 1000 ]</strong><br>Default: 50<br>Number of items per page</p>          | 50                                             |
| direction           | <p><strong>string</strong></p><p>Default: "ASC"</p><p>Enum: "ASC" "DESC"</p><p>Sort direction</p> | ASC                                            |
| cursor              | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination</p>            |                                                |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "folders": [],
    "files": [],
    "total_files": 0,
    "total_folders": 0,
    "cursor": null,
    "breadcrumbs": [],
    "permission_previews": [
        "VIEW",
        "EDIT",
        "UPLOAD",
        "DELETE",
        "INVITE",
        "MANAGE"
    ]
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

|          | type                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Request  | [IRequestListDirectory](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L200)  |
| Response | [IResponseListDirectory](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L218) |

***

## Directory Actions&#x20;

Perform actions on files and folders such as get, create, update, delete, copy, move, and restore

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/directory/action
```

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

| actions <mark style="color:red;">(required)</mark> | <p><strong>Array of objects (DirectoryAction)</strong><br>List of directory actions to execute</p> |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------- |

```json
{
  "actions": [
    {
      // Required: The operation to perform (e.g., DELETE_FOLDER, MOVE_FILE, CREATE_FOLDER)
      "action": "DELETE_FOLDER",
      
      // Optional: Target resource - use either path OR id
      "target": {
        "resource_path": "/path/to/resource",  // Full path to file/folder
        "resource_id": "FolderID_abc123"       // Unique ID (FileID_<id> or FolderID_<id>)
      },
      
      // Required: Action-specific data
      "payload": {
        // Payload content varies by action type
        // Common fields: destination_path, overwrite, permissions, metadata
      }
    }
  ]
}
```

</details>

**Typescript Types**

|          | type                                                                                                                                   |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Request  | [IRequestDirectoryAction](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L229)  |
| Response | [IResponseDirectoryAction](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L234) |

#### Refer [directory-actions.md](directory-actions.md "mention") for detailed request body schema

####
