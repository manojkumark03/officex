---
description: Virtual Hierarchical Filesystem
---

# Directory Filesystem

OfficeX storage uses a virtual filesystem representation for files & folders, not a flat S3-like prefix key. In this guide we will learn how to navigate it.

First let's examine what a `File` and `Folder` looks like:

```typescript

import { FileRecord, FolderRecord } from "officexapp/types";

export interface FileRecord {
  id: FileID;
  name: string;
  parent_folder_uuid: FolderID;
  file_version: number;
  prior_version?: FileID;
  next_version?: FileID;
  extension: string;
  full_directory_path: DriveFullFilePath; // private string, this may be redacted when sent to frontend
  labels: LabelValue[];
  created_by: UserID;
  created_at: number;
  disk_id: DiskID;
  disk_type: DiskTypeEnum;
  file_size: number;
  raw_url: string;
  last_updated_date_ms: number;
  last_updated_by: UserID;
  deleted: boolean;
  drive_id: ICPPrincipalString;
  expires_at: number;
  restore_trash_prior_folder_uuid?: FolderID;
  has_sovereign_permissions: boolean;
  shortcut_to?: FileID;
  upload_status: UploadStatus;
  external_id?: ExternalID;
  external_payload?: ExternalPayload;
  version_id: FileVersionID;
  notes?: string;
}

export interface FolderRecord {
  id: FolderID;
  name: string;
  parent_folder_uuid?: FolderID;
  subfolder_uuids: FolderID[];
  file_uuids: FileID[];
  full_directory_path: DriveFullFilePath; // private string, this may be redacted when sent to frontend
  labels: LabelValue[];
  created_by: UserID;
  created_at: number;
  last_updated_date_ms: number;
  last_updated_by: UserID;
  disk_id: DiskID;
  disk_type: DiskTypeEnum;
  deleted: boolean;
  expires_at: number;
  drive_id: DriveID;
  restore_trash_prior_folder_uuid?: FolderID;
  has_sovereign_permissions: boolean;
  shortcut_to?: FolderID;
  external_id?: ExternalID;
  external_payload?: ExternalPayload;
  notes?: string;
}
```



### Navigation

### Redaction

### Versioning

### Conflict Resolution Strategy

### File Destination Routing

```typescript
GET /v1/drive/:org_id/directory/asset/:file_id_with_extension
```









