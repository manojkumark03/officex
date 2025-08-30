---
description: Data types and models used throughout the API. See POST /directory/actions
---

# Directory Actions

## Get File

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/eifafaf/drive-org-id-directory-action-view-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, GetFileAction, GetFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type GetFileAction {
      // Required: The operation to perform
      "action": "GET_FILE",
      // Optional: Target resource - omit when querying "shared with me" resources
      // Server will find all shared files/folders (some unreachable directly)
      // "target": {
      //   "resource_path": "DiskID::/documents/project/", // Full path to file/folder
      //   "resource_id": "FolderID_xyz789" // Unique ID (FileID_<id> or FolderID_<id>)
      // },
      // Required: Action-specific data
      "payload": type GetFilePayload {
        "id": "{{file_id}}", // Target file ID
        "share_track_hash"?: "track456" // Hash for share tracking
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import {IResponseDirectoryAction, DirectoryActionOutcome, GetFileAction, GetFileResponse, FileRecordFE, FilePathBreadcrumb } from "officexapp/types"

type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type GetFileAction {
      "action": "GET_FILE",
      "payload": {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
        "share_track_hash": "track123"
      }
    },
    "response": {
      "result": type GetFileResponse {
        "file": type FileRecordFE {
          "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
          "name": "download.jpeg",
          "parent_folder_uuid": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
          "version_id": "FileVersionID_2bfa2c8a-2ecd-42c3-a157-65d7e48ad103",
          "extension": "jpeg",
          "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/mine aws/download.jpeg",
          "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "created_at": 1755589485206,
          "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
          "disk_type": "AWS_BUCKET",
          "file_size": 11242,
          "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_af475a5a-6699-4f37-9305-22d96ca09111.jpeg",
          "deleted": false,
          "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
          "upload_status": "COMPLETED",
          "expires_at": -1,
          "restore_trash_prior_folder_uuid": "",
          "has_sovereign_permissions": false,
          "shortcut_to": null,
          "notes": "",
          "external_id": "",
          "external_payload": "",
          "file_version": 1,
          "labels": [],
          "last_updated_date_ms": 1755589487514,
          "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::../download.jpeg",
          "permission_previews": [
            "VIEW",
            "EDIT", 
            "UPLOAD",
            "DELETE",
            "INVITE",
            "MANAGE"
          ]
        },
        "breadcrumbs": [
          type FilePathBreadcrumb {
            "resource_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
            "resource_name": "Amazon Storage Generic Vendor",
            "visibility_preview": [
              "PRIVATE_MODIFY"
            ]
          },
          type FilePathBreadcrumb {
            "resource_id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
            "resource_name": "mine aws",
            "visibility_preview": []
          },
          type FilePathBreadcrumb {
            "resource_id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
            "resource_name": "download.jpeg",
            "visibility_preview": []
          }
        ]
      }
    }
  }
]
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

***

## Get Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/kv31yfl/drive-org-id-directory-action-view-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, GetFolderAction, GetFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type GetFolderAction {
      // Required: The operation to perform
      "action": "GET_FOLDER",
      // Optional: Target resource - omit when querying "shared with me" resources
      // Server will find all shared files/folders (some unreachable directly)
      // "target": {
      //   "resource_path": "DiskID::/documents/project/",  // Full path to file/folder
      //   "resource_id": "FolderID_xyz789"                 // Unique ID (FileID_<id> or FolderID_<id>)
      // },
      // Required: Action-specific data
      "payload": type GetFolderPayload {
        "id": "{{folder_id}}", // Target folder ID
        "share_track_hash"?: "track456" // Hash for share tracking
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, GetFolderAction, GetFolderResponse, FolderRecordFE, FilePathBreadcrumb } from "officexapp/types"

type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type GetFolderAction {
      "action": "GET_FOLDER",
      "payload": {
        "id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
        "share_track_hash": "track123"
      }
    },
    "response": {
      "result": type GetFolderResponse {
        "folder": type FolderRecordFE {
          "id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
          "name": "mine aws",
          "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
          "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/mine aws/",
          "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "created_at": 1755588916504,
          "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
          "disk_type": "AWS_BUCKET",
          "deleted": false,
          "expires_at": -1,
          "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
          "restore_trash_prior_folder_uuid": null,
          "has_sovereign_permissions": false,
          "shortcut_to": null,
          "notes": null,
          "external_id": null,
          "external_payload": null,
          "subfolder_uuids": "[]",
          "file_uuids": "[\"FileID_af475a5a-6699-4f37-9305-22d96ca09111\"]",
          "labels": [],
          "last_updated_date_ms": 1755588938944,
          "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::mine aws/",
          "permission_previews": [
            "VIEW",
            "EDIT",
            "UPLOAD",
            "DELETE",
            "INVITE",
            "MANAGE"
          ]
        },
        "breadcrumbs": [
          type FilePathBreadcrumb {
            "resource_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
            "resource_name": "Amazon Storage Generic Vendor",
            "visibility_preview": [
              "PRIVATE_MODIFY"
            ]
          },
          type FilePathBreadcrumb {
            "resource_id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
            "resource_name": "mine aws",
            "visibility_preview": []
          }
        ]
      }
    }
  }
]
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

***

## Create File

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/9j4r1zl/drive-org-id-directory-action-create-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, CreateFileAction, CreateFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type CreateFileAction {
      // Required: The operation to perform
      "action": "CREATE_FILE",
      // Required: File creation data
      "payload": type CreateFilePayload {
        // Optional: Unique file ID (auto-generated if omitted)
        // "id"?: "FileID_abc123",
        "name": "Proposal", // Required: File name
        "parent_folder_uuid": "{{folder_id}}", // Required: ID of the parent folder
        "extension": "pdf", // Required: File extension
        "labels": [], // Required: Labels to associate with the file
        "file_size": 124434, // Required: Size in bytes
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939", // Required: ID of the disk where the file will be stored
        "disk_type": "AWS_BUCKET", // Required: Type of disk storage
        // Optional fields:
        // "expires_at"?: 1735689600, // Timestamp when the file expires
        // "file_conflict_resolution"?: "rename", // How to handle file name conflicts
        // "has_sovereign_permissions"?: false, // Whether the file has sovereign permissions
        // "shortcut_to"?: "FileID_xyz789", // ID of the file to create a shortcut to
        // "external_id"?: "ext_12345", // External identifier for integration purposes
        // "external_payload"?: {}, // Additional data for external integrations
        // "raw_url"?: "https://example.com/file.pdf", // URL where the raw file content can be accessed
        // "notes"?: "Project proposal document" // Additional notes about the file
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { DirectoryActionOutcome, GetFileAction, DirectoryActionResponse, CreateFileResponse, FileRecord } from "officexapp/types"

type DirectoryActionResponseBody {
    data: [
        type DirectoryActionOutcome {
            "id": string,
            "success": true,
            "request": type GetFileAction {
                "action": "CREATE_FILE",
                "payload": {
                    "name": "Proposal",
                    "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "extension": "pdf",
                    "labels": [],
                    "file_size": 124434,
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET"
                }
            },
            "response": type DirectoryActionResponse {
                "result": type CreateFileResponse {
                    "file": type FileRecord {
                        "id": "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa",
                        "name": "Proposal",
                        "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                        "version_id": "FileVersionID_13ca3558-c1e3-4f0c-983e-b086cf95a55e",
                        "file_version": 1,
                        "extension": "Proposal",
                        "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Proposal",
                        "labels": [],
                        "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                        "created_at": 1755590323356,
                        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                        "disk_type": "AWS_BUCKET",
                        "file_size": 124434,
                        "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa.Proposal",
                        "last_updated_date_ms": 1755590323356,
                        "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                        "deleted": false,
                        "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                        "expires_at": -1,
                        "has_sovereign_permissions": false,
                        "upload_status": "QUEUED",
                        "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Proposal",
                        "permission_previews": [
                            "VIEW",
                            "EDIT",
                            "UPLOAD",
                            "DELETE",
                            "INVITE",
                            "MANAGE"
                        ]
                    },
                    "upload": {
                        "url": "https://s3.amazonaws.com/officex-customerpurchaseid-92b68f13-93f3-4856-9283-d0f908b5c633",
                        "fields": {
                            "key": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939/FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa/FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa.Proposal",
                            "acl": "private",
                            "Content-Disposition": "inline",
                            "x-amz-algorithm": "AWS4-HMAC-SHA256",
                            "x-amz-credential": "AKIAXRT2PYYNLCFMDDO6/20250819/us-east-1/s3/aws4_request",
                            "x-amz-date": "20250819T075843Z",
                            "policy": "eyJleHBpcmF0aW9uIjoiMjAyNS0wOC0yMFQwNzo1ODo0M1oiLCJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJvZmZpY2V4LWN1c3RvbWVycHVyY2hhc2VpZC05MmI2OGYxMy05M2YzLTQ4NTYtOTI4My1kMGY5MDhiNWM2MzMifSx7ImtleSI6IkRyaXZlSURfY3ZkZzYta3BncnUtM2ZvaGwtem5yM3AtZHgzZ2ctZW0zcWstcXlxb3ktZ3Fkcmstd2c3bjItdWZhNGQtYmFlL0Rpc2tJRF9kMmIxZmVjOS1lYmY4LTRjYTUtYWRiMy04ZGVhOTM5NDE5MzkvRmlsZUlEX2IyNzA1ZjBkLTlmYWEtNDc2ZS04NGI0LWIwYmFjYWEzMzNhYS9GaWxlSURfYjI3MDVmMGQtOWZhYS00NzZlLTg0YjQtYjBiYWNhYTMzM2FhLlByb3Bvc2FsIn0seyJhY2wiOiJwcml2YXRlIn0sWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsMCwiMTI0NDM0Il0seyJ4LWFtei1hbGdvcml0aG0iOiJBV1M0LUhNQUMtU0hBMjU2In0seyJ4LWFtei1jcmVkZW50aWFsIjoiQUtJQVhSVDJQWVlOTENGTURETzYvMjAyNTA4MTkvdXMtZWFzdC0xL3MzL2F3czRfcmVxdWVzdCJ9LHsieC1hbXotZGF0ZSI6IjIwMjUwODE5VDA3NTg0M1oifSx7IkNvbnRlbnQtRGlzcG9zaXRpb24iOiJpbmxpbmUifV19",
                            "x-amz-signature": "51dc317872a8edaa7eb51ae258bcf7b025b6bc78b61a9e990bd8034c48586bec"
                        }
                    },
                    "notes": "File created successfully"
                }
            }
        }
    ]
]
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

***

## Create Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/dhwq91s/drive-org-id-directory-action-create-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, CreateFolderAction, CreateFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type CreateFolderAction {
      // Required: The operation to perform
      "action": "CREATE_FOLDER",
      // Required: Folder creation data
      "payload": type CreateFolderPayload {
        // Optional: Unique folder ID (auto-generated if omitted)
        // "id"?: "FolderID_abc123",
        "name": "Investigation", // Required: Name of the folder
        "labels": [], // Required: Labels to associate with the folder
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939", // Required: ID of the disk where the folder will be stored
        "disk_type": "AWS_BUCKET", // Required: Type of disk storage
        "parent_folder_uuid": "{{root_folder}}", // Required: ID of the parent folder
        // Optional fields:
        // "expires_at"?: 1735689600, // Timestamp when the folder expires
        // "file_conflict_resolution"?: "rename", // How to handle file name conflicts
        // "has_sovereign_permissions"?: false, // Whether the folder has sovereign permissions
        // "shortcut_to"?: "FolderID_xyz789", // ID of the folder to create a shortcut to
        // "external_id"?: "ext_12345", // External identifier for integration purposes
        // "external_payload"?: {}, // Additional data for external integrations
        // "notes"?: "Investigation project folder" // Additional notes about the folder
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import {  IResponseDirectoryAction, DirectoryActionOutcome, CreateFolderAction, CreateFolderResponse, FolderRecordFE } from "officexapp/types"

type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type CreateFolderAction {
      "action": "CREATE_FOLDER",
      "payload": {
        "name": "Investigation",
        "labels": [],
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
        "disk_type": "AWS_BUCKET",
        "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a"
      }
    },
    "response": {
      "result": type CreateFolderResponse {
        "folder": type FolderRecordFE {
          "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
          "name": "Investigation",
          "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
          "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Investigation/",
          "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "created_at": 1755590718251,
          "subfolder_uuids": "[]",
          "file_uuids": "[]",
          "last_updated_date_ms": 1755590718251,
          "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
          "disk_type": "AWS_BUCKET",
          "deleted": 0,
          "expires_at": -1,
          "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
          "restore_trash_prior_folder_uuid": null,
          "has_sovereign_permissions": 0,
          "shortcut_to": null,
          "notes": null,
          "external_id": null,
          "external_payload": null,
          "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Investigation/",
          "permission_previews": [
            "VIEW",
            "EDIT",
            "UPLOAD",
            "DELETE",
            "INVITE",
            "MANAGE"
          ]
        },
        "notes": "Folder created successfully"
      }
    }
  }
]
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

***

## Update File&#x20;

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ynx2wxl/drive-org-id-directory-action-edit-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, UpdateFileAction, UpdateFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type UpdateFileAction {
      // Required: The operation to perform
      "action": "UPDATE_FILE",
      // Required: File update data
      "payload": type UpdateFilePayload {
        "id": "{{file_id}}", // Required: File ID to update
        "name"?: "Revised Proposal", // Optional: New name for the file
        // Optional fields:
        // "labels"?: ["important", "draft"], // New labels for the file
        // "upload_status"?: "completed", // New upload status
        // "raw_url"?: "https://example.com/file.pdf", // New URL where the raw file content can be accessed
        // "expires_at"?: 1735689600, // New expiration timestamp
        // "external_id"?: "ext_12345", // External identifier for integration purposes
        // "external_payload"?: {}, // Additional data for external integrations
        // "notes"?: "Updated proposal document", // Additional notes about the file
        // "shortcut_to"?: "FileID_xyz789", // ID of the file to create a shortcut to
        // "request_presigned_url"?: true // Whether to request a presigned upload URL for the file (used for updating)
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, UpdateFileAction, UpdateFileResponse, FileRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type UpdateFileAction {
      "action": "UPDATE_FILE",
      "payload": {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
        "name": "Revised Proposal"
      }
    },
    "response": {
      "result": type UpdateFileResponse {
        "file": type FileRecordFE {
          "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
          "name": "Revised Proposal",
          "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
          "version_id": "FileVersionID_2bfa2c8a-2ecd-42c3-a157-65d7e48ad103",
          "extension": "jpeg",
          "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Proposal",
          "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "created_at": 1755589485206,
          "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
          "disk_type": "AWS_BUCKET",
          "file_size": 11242,
          "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_af475a5a-6699-4f37-9305-22d96ca09111.jpeg",
          "deleted": false,
          "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
          "upload_status": "COMPLETED",
          "expires_at": -1,
          "restore_trash_prior_folder_uuid": null,
          "has_sovereign_permissions": false,
          "shortcut_to": null,
          "notes": "",
          "external_id": "",
          "external_payload": "",
          "file_version": 1,
          "labels": [],
          "last_updated_date_ms": 1755935916460,
          "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Revised Proposal",
          "permission_previews": [
            "VIEW",
            "EDIT",
            "UPLOAD",
            "DELETE",
            "INVITE",
            "MANAGE"
          ]
        },
        "notes": ""
      }
    }
  }
]
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

***

## Update Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ljy58xr/drive-org-id-directory-action-edit-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, UpdateFolderAction, UpdateFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type UpdateFolderAction {
      // Required: The operation to perform
      "action": "UPDATE_FOLDER",
      // Required: Folder update data
      "payload": type UpdateFolderPayload {
        "id": "{{folder_id}}", // Required: Folder ID to update
        "name"?: "Revised Investigation", // Optional: New name for the folder
        // Optional fields:
        // "labels"?: ["important", "active"], // New labels for the folder
        // "expires_at"?: 1735689600, // New expiration timestamp
        // "external_id"?: "ext_12345", // External identifier for integration purposes
        // "external_payload"?: {}, // Additional data for external integrations
        // "notes"?: "Updated investigation folder", // Additional notes about the folder
        // "shortcut_to"?: "FolderID_xyz789" // ID of the folder to create a shortcut to
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, UpdateFolderAction, UpdateFolderResponse, FolderRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type UpdateFolderAction {
      "action": "UPDATE_FOLDER",
      "payload": {
        "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "name": "Revised Investigation"
      }
    },
    "response": {
      "result": type UpdateFolderResponse {
        "folder": type FolderRecordFE {
          "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
          "name": "Revised Investigation",
          "parent_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
          "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation/",
          "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "created_at": 1755590718251,
          "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
          "disk_type": "AWS_BUCKET",
          "deleted": false,
          "expires_at": -1,
          "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
          "restore_trash_prior_folder_uuid": null,
          "has_sovereign_permissions": false,
          "shortcut_to": null,
          "notes": null,
          "external_id": null,
          "external_payload": null,
          "subfolder_uuids": "[]",
          "file_uuids": "[]",
          "labels": [],
          "last_updated_date_ms": 1755591034700,
          "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
          "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Revised Investigation/",
          "permission_previews": [
            "VIEW",
            "EDIT",
            "UPLOAD",
            "DELETE",
            "INVITE",
            "MANAGE"
          ]
        }
      }
    }
  }
]
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

***

## Delete File

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/cry6ff9/drive-org-id-directory-action-delete-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, DeleteFileAction, DeleteFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type DeleteFileAction {
      // Required: The operation to perform
      "action": "DELETE_FILE",
      // Required: File deletion data
      "payload": type DeleteFilePayload {
        "id": "{{file_id}}", // Required: File ID to delete
        "permanent": false // Required: Whether to permanently delete the file or move it to trash
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, DeleteFileAction, DeleteFileResponse } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type DeleteFileAction {
      "action": "DELETE_FILE",
      "payload": {
        "id": "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa",
        "permanent": false
      }
    },
    "response": {
      "result": type DeleteFileResponse {
        "file_id": "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa",
        "path_to_trash": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/Revised Proposal"
      }
    }
  }
]
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

***

## Delete Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/ihckq0x/drive-org-id-directory-action-delete-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, DeleteFolderAction, DeleteFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type DeleteFolderAction {
      // Required: The operation to perform
      "action": "DELETE_FOLDER",
      // Required: Folder deletion data
      "payload": type DeleteFolderPayload {
        "id": "{{folder_id}}", // Required: Folder ID to delete
        "permanent": false // Required: Whether to permanently delete the folder or move it to trash
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, DeleteFolderAction, DeleteFolderResponse } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type DeleteFolderAction {
      "action": "DELETE_FOLDER",
      "payload": {
        "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "permanent": false
      }
    },
    "response": {
      "result": type DeleteFolderResponse {
        "folder_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "path_to_trash": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/Revised Investigation/",
        "deleted_files": [],
        "deleted_folders": []
      }
    }
  }
]
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

***

## Copy File

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/py5phg8/drive-org-id-directory-action-copy-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, CopyFileAction, CopyFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type CopyFileAction {
      // Required: The operation to perform
      "action": "COPY_FILE",
      // Required: File copy data
      "payload": type CopyFilePayload {
        "id": "{{file_id}}", // Required: File ID to copy
        "destination_folder_id"?: "{{alt_folder_id}}", // Optional: ID of the destination folder
        // Optional fields:
        // "destination_folder_path"?: "/backup/files", // Path to the destination folder
        // "file_conflict_resolution"?: "rename" // How to handle file name conflicts ("rename", "overwrite", "skip")
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, CopyFileAction, CopyFileResponse, FileRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type CopyFileAction {
      "action": "COPY_FILE",
      "payload": {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
        "destination_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a"
      }
    },
    "response": {
      "result": type FileRecordFE {
        "id": "FileID_a98bfde3-5edf-48de-b774-29285208d1cb",
        "name": "download.jpeg",
        "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
        "version_id": "FileVersionID_ecc638b6-95dd-4960-ab41-44588dbd953b",
        "extension": "jpeg",
        "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/download.jpeg",
        "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "created_at": 1755591693465,
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
        "disk_type": "AWS_BUCKET",
        "file_size": 11242,
        "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_a98bfde3-5edf-48de-b774-29285208d1cb.jpeg",
        "last_updated_date_ms": 1755591693465,
        "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "deleted": 0,
        "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
        "upload_status": "COMPLETED",
        "expires_at": -1,
        "restore_trash_prior_folder_uuid": null,
        "has_sovereign_permissions": 0,
        "shortcut_to": null,
        "notes": "",
        "external_id": "",
        "external_payload": "",
        "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::download.jpeg",
        "permission_previews": [
          "VIEW",
          "EDIT",
          "UPLOAD",
          "DELETE",
          "INVITE",
          "MANAGE"
        ]
      }
    }
  }
]
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

***

## Copy Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/qfba5du/drive-org-id-directory-action-copy-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, CopyFolderAction, CopyFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type CopyFolderAction {
      // Required: The operation to perform
      "action": "COPY_FOLDER",
      // Required: Folder copy data
      "payload": type CopyFolderPayload {
        "id": "{{folder_id}}", // Required: Folder ID to copy
        "destination_folder_id"?: "{{alt_folder_id}}", // Optional: ID of the destination folder
        // Optional fields:
        // "destination_folder_path"?: "/backup/folders", // Path to the destination folder
        // "file_conflict_resolution"?: "rename" // How to handle file name conflicts ("rename", "overwrite", "skip")
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, CopyFolderAction, CopyFolderResponse, FolderRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type CopyFolderAction {
      "action": "COPY_FOLDER",
      "payload": {
        "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "destination_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a"
      }
    },
    "response": {
      "result": type FolderRecordFE {
        "id": "FolderID_7403fbbf-3cac-486f-8d93-80d6eed8bcbf",
        "name": "Revised Investigation",
        "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
        "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation/",
        "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "created_at": 1755591836489,
        "subfolder_uuids": null,
        "file_uuids": null,
        "last_updated_date_ms": 1755591836489,
        "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
        "disk_type": "AWS_BUCKET",
        "deleted": 0,
        "expires_at": -1,
        "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
        "restore_trash_prior_folder_uuid": null,
        "has_sovereign_permissions": 0,
        "shortcut_to": null,
        "notes": null,
        "external_id": null,
        "external_payload": null,
        "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Revised Investigation/",
        "permission_previews": [
          "VIEW",
          "EDIT",
          "UPLOAD",
          "DELETE",
          "INVITE",
          "MANAGE"
        ]
      }
    }
  }
]
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

***

## Move File

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/o97xt4p/drive-org-id-directory-action-move-file?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, MoveFileAction, MoveFilePayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type MoveFileAction {
      // Required: The operation to perform
      "action": "MOVE_FILE",
      // Required: File move data
      "payload": type MoveFilePayload {
        "id": "{{file_id}}", // Required: File ID to move
        "destination_folder_id"?: "{{alt_folder_id}}", // Optional: ID of the destination folder
        // Optional fields:
        // "destination_folder_path"?: "/new/location", // Path to the destination folder
        // "file_conflict_resolution"?: "rename" // How to handle file name conflicts ("rename", "overwrite", "skip")
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, MoveFileAction, MoveFileResponse, FileRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type MoveFileAction {
      "action": "MOVE_FILE",
      "payload": {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
        "destination_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a"
      }
    },
    "response": {
      "result": type FileRecordFE {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
        "name": "download (2).jpeg",
        "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
        "version_id": "FileVersionID_2bfa2c8a-2ecd-42c3-a157-65d7e48ad103",
        "extension": "jpeg",
        "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/download (2).jpeg",
        "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "created_at": 1755589485206,
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
        "disk_type": "AWS_BUCKET",
        "file_size": 11242,
        "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_af475a5a-6699-4f37-9305-22d96ca09111.jpeg",
        "last_updated_date_ms": 1755591969722,
        "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "deleted": 0,
        "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
        "upload_status": "COMPLETED",
        "expires_at": -1,
        "restore_trash_prior_folder_uuid": "",
        "has_sovereign_permissions": 0,
        "shortcut_to": null,
        "notes": "",
        "external_id": "",
        "external_payload": "",
        "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::download (2).jpeg",
        "permission_previews": [
          "VIEW",
          "EDIT",
          "UPLOAD",
          "DELETE",
          "INVITE",
          "MANAGE"
        ]
      }
    }
  }
]
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

***

## Move Folder

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/8j3s7ms/drive-org-id-directory-action-move-folder?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, MoveFolderAction, MoveFolderPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type MoveFolderAction {
      // Required: The operation to perform
      "action": "MOVE_FOLDER",
      // Required: Folder move data
      "payload": type MoveFolderPayload {
        "id": "{{folder_id}}", // Required: Folder ID to move
        "destination_folder_id"?: "{{alt_folder_id}}", // Optional: ID of the destination folder
        // Optional fields:
        // "destination_folder_path"?: "/new/location", // Path to the destination folder
        // "file_conflict_resolution"?: "rename" // How to handle file name conflicts ("rename", "overwrite", "skip")
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, MoveFolderAction, MoveFolderResponse, FolderRecordFE } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type MoveFolderAction {
      "action": "MOVE_FOLDER",
      "payload": {
        "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "destination_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a"
      }
    },
    "response": {
      "result": type FolderRecordFE {
        "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
        "name": "Revised Investigation (2)",
        "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
        "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2)/",
        "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "created_at": 1755590718251,
        "subfolder_uuids": "[]",
        "file_uuids": "[]",
        "last_updated_date_ms": 1755592087951,
        "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
        "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
        "disk_type": "AWS_BUCKET",
        "deleted": 1,
        "expires_at": -1,
        "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
        "restore_trash_prior_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
        "has_sovereign_permissions": 0,
        "shortcut_to": null,
        "notes": null,
        "external_id": null,
        "external_payload": null,
        "clipped_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::Revised Investigation (2)/",
        "permission_previews": [
          "VIEW",
          "EDIT",
          "UPLOAD",
          "DELETE",
          "INVITE",
          "MANAGE"
        ]
      }
    }
  }
]
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

***

## Restore Trash

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/z4vfceq/drive-org-id-directory-action-restore-trash?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

Request Schema

```typescript
import { IRequestDirectoryAction, RestoreTrashAction, RestoreTrashPayload } from "officexapp/types"

// Request Body Type
type DirectoryActionRequestBody = IRequestDirectoryAction {
  "actions": [
    type RestoreTrashAction {
      // Required: The operation to perform
      "action": "RESTORE_TRASH",
      // Required: File restore data
      "payload": type RestoreTrashPayload {
        "id": "{{file_id}}", // Required: File ID or Folder ID to restore from trash
        // Optional fields:
        // "file_conflict_resolution"?: "rename", // How to handle file conflicts during restore ("rename", "overwrite", "skip")
        // "restore_to_folder_path"?: "/documents" // Custom path to restore to (if not using original path)
      }
    }
  ]
}
```

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```typescript
import { IResponseDirectoryAction, DirectoryActionOutcome, RestoreTrashAction, RestoreTrashResponse } from "officexapp/types"

// Response Body Type
type DirectoryActionResponse = IResponseDirectoryAction [
  type DirectoryActionOutcome {
    "success": true,
    "request": type RestoreTrashAction {
      "action": "RESTORE_TRASH",
      "payload": {
        "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111"
      }
    },
    "response": {
      "result": type RestoreTrashResponse {
        "restored_folders": [],
        "restored_files": [
          "FileID_af475a5a-6699-4f37-9305-22d96ca09111"
        ]
      }
    }
  }
]
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

***
