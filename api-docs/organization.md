---
description: Operations for managing own drive canister
---

# Organization

## Overview

<details>

<summary></summary>

```typescript
const organizationRoutes: FastifyPluginAsync = async (
  fastify,
  opts
): Promise<void> => {
  // GET /v1/drive/:org_id/organization/about
  // use to get info about the org
  fastify.get<{ Params: OrgIdParams; Reply: IAboutDriveResponseData }>(
    `/about`,
    { preHandler: [driveRateLimitPreHandler] },
    aboutDriveHandler
  );

  // GET /v1/drive/:org_id/organization/snapshot
  // developer route for debugging. disabled in prod
  fastify.get<{ Params: OrgIdParams }>(
    `/snapshot`,
    { preHandler: [driveRateLimitPreHandler] },
    snapshotDriveHandler
  );

  // POST /v1/drive/:org_id/organization/replay
  // can skip this one, its for auditable time travel
  fastify.post<{ Params: OrgIdParams; Body: IRequestReplayDrive }>(
    `/replay`,
    { preHandler: [driveRateLimitPreHandler] },
    replayDriveHandler
  );

  // POST /v1/drive/:org_id/organization/search
  // to search across organization by string
  fastify.post<{ Params: OrgIdParams; Body: IRequestSearchDrive }>(
    `/search`,
    { preHandler: [driveRateLimitPreHandler] },
    searchDriveHandler
  );

  // POST /v1/drive/:org_id/organization/reindex
  // to reindex the search universe
  fastify.post<{ Params: OrgIdParams; Body: IRequestReindexDrive }>(
    `/reindex`,
    { preHandler: [driveRateLimitPreHandler] },
    reindexDriveHandler
  );

  // POST /v1/drive/:org_id/organization/transfer_ownership
  // transfer ownership to another user
  fastify.post<{ Params: OrgIdParams; Body: IRequestTransferDriveOwnership }>(
    `/transfer_ownership`,
    { preHandler: [driveRateLimitPreHandler] },
    transferOwnershipDriveHandler
  );

  // POST /v1/drive/:org_id/organization/update_allowed_domains
  // Skip this one, full custom domains coming soon
  fastify.post(
    `/update_allowed_domains`,
  
    updateAllowedDomainsDriveHandler
  );

  // GET /v1/drive/:org_id/organization/whoami
  // Checks who an api key is
  fastify.get<{ Params: OrgIdParams; Reply: IResponseWhoAmI }>(
    `/whoami`,
    { preHandler: [driveRateLimitPreHandler] },
    whoAmIDriveHandler
  );

  // POST /v1/drive/:org_id/organization/superswap_user
  // Swaps a user completely throughout entire database, used to redeem placeholder contacts
  // ONLY superswaps in your database, not others
  fastify.post<{ Params: OrgIdParams; Body: IRequestSuperswapUser }>(
    `/superswap_user`,
    { preHandler: [driveRateLimitPreHandler] },
    superswapUserIdDriveHandler
  );

  // POST /v1/drive/:org_id/organization/redeem
  // Activate a fresh new organization
  fastify.post<{ Params: OrgIdParams; Body: IRequestRedeemOrg }>(
    `/redeem`,
    { preHandler: [driveRateLimitPreHandler] },
    redeemOrganizationDriveHandler
  );

  // POST /v1/drive/:org_id/organization/inbox
  // Webhook endpoint that can be programmed on
  fastify.post<{ Params: OrgIdParams; Body: IRequestInboxOrg }>(
    `/inbox`,
    { preHandler: [driveRateLimitPreHandler] },
    inboxDriveHandler
  );

  // POST /v1/drive/:org_id/organization/shortlink
  // built-in url shortener
  fastify.post<{ Params: OrgIdParams; Body: IRequestShortLink }>(
    `/shortlink`,
    { preHandler: [driveRateLimitPreHandler] },
    shortlinkHandler
  );
};

export default organizationRoutes;

```

</details>

## Get Snapshot

Developer route for debugging. disabled in prod

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/organization/snapshot
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/uvvon89/organization-snapshot?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p> | DriveID\_abc123 |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------- |

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
            "DRIVE_ID": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
            "CANISTER_ID": "cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
            "VERSION": "OfficeX.Web2_Beta.1.0",
            "OWNER_ID": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "URL_ENDPOINT": "https://officex.otterpad.cc",
            "DRIVE_STATE_TIMESTAMP_NS": 1755581408331,
            "EXTERNAL_ID_MAPPINGS": {},
            "RECENT_DEPLOYMENTS": [],
            "SPAWN_REDEEM_CODE": "",
            "SPAWN_NOTE": "giftcard GiftcardSpawnOrgID_5df5d6cd-89d0-4f75-9d67-01f155af92bb was redeemed to spawn drive with 3500000000000 cycles, owned by UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae, on timestamp_ms 1755581408331 2025-08-19T05:30:08.331Z",
            "NONCE_UUID_GENERATED": "0",
            "UUID_CLAIMED": {
                "PurchaseID_32164a50-bf48-4d8d-9d13-a7fde18712db": true,
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939": true,
                "FileID_a98bfde3-5edf-48de-b774-29285208d1cb": true,
                "FolderID_7403fbbf-3cac-486f-8d93-80d6eed8bcbf": true,
                "DirectoryPermissionID_bddd1bb7-f292-448a-a9dc-6a82bb88627f": true,
                "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a": true,
                "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b": true,
                "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37": true,
                "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739": true,
                "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591": true,
                "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7": true,
                "SystemPermissionID_0298d45b-561a-4abe-8f16-2255cca5896a": true,
                "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae": true,
                "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957": true,
                "ApiKeyID_b9cfb179-f01b-4f23-a9bd-313211815c4c": true
            },
            "APIKEYS_BY_VALUE_HASHTABLE": {
                "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJhMDg0MzFkYmUwZjJjOGFmODk5ODQ3ZjE0ZTYyODBjYmRjMjYzZmIzZTYxMWVhNDU1YTBmMmViNmZiYTIxNjIwIn0=": "ApiKeyID_cf9d71d5-99c1-4a41-baed-46e09610e269",
                "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJjMjZmYTNhZGQ5NGMxMWVjNjY3Njk2OWIxOGRiOTZiNmNmYTI0Y2ZhZmYwYjI0MGY0ZDU4MmFhOTI0NTlkNTA5In0=": "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957"
            },
            "APIKEYS_BY_ID_HASHTABLE": {
                "ApiKeyID_cf9d71d5-99c1-4a41-baed-46e09610e269": {
                    "id": "ApiKeyID_cf9d71d5-99c1-4a41-baed-46e09610e269",
                    "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJhMDg0MzFkYmUwZjJjOGFmODk5ODQ3ZjE0ZTYyODBjYmRjMjYzZmIzZTYxMWVhNDU1YTBmMmViNmZiYTIxNjIwIn0=",
                    "user_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "name": "Default Admin Key for Spawned Drive",
                    "private_note": null,
                    "created_at": 1755581408912,
                    "begins_at": 1755581408912,
                    "expires_at": -1,
                    "is_revoked": 0,
                    "external_id": null,
                    "external_payload": null
                },
                "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957": {
                    "id": "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957",
                    "value": "eyJhdXRoX3R5cGUiOiJBUElfS0VZIiwidmFsdWUiOiJjMjZmYTNhZGQ5NGMxMWVjNjY3Njk2OWIxOGRiOTZiNmNmYTI0Y2ZhZmYwYjI0MGY0ZDU4MmFhOTI0NTlkNTA5In0=",
                    "user_id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                    "name": "My API Key",
                    "private_note": null,
                    "created_at": 1756124773388,
                    "begins_at": 1756124773388,
                    "expires_at": -1,
                    "is_revoked": 0,
                    "external_id": null,
                    "external_payload": null
                }
            },
            "USERS_APIKEYS_HASHTABLE": {
                "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae": [
                    "ApiKeyID_cf9d71d5-99c1-4a41-baed-46e09610e269"
                ],
                "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae": [
                    "ApiKeyID_fed8deb5-d94e-4509-8e4d-3d3467efc957"
                ]
            },
            "CONTACTS_BY_ID_HASHTABLE": {
                "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae": {
                    "id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "name": "Owner",
                    "avatar": null,
                    "email": null,
                    "notifications_url": null,
                    "public_note": null,
                    "private_note": null,
                    "secret_entropy": null,
                    "evm_public_address": "",
                    "icp_principal": "3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "seed_phrase": null,
                    "from_placeholder_user_id": null,
                    "redeem_code": "REDEEM_1755581408331",
                    "created_at": 1755581408331,
                    "last_online_ms": 1756136764106,
                    "external_id": null,
                    "external_payload": null
                },
                "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae": {
                    "id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                    "name": "user2",
                    "avatar": "",
                    "email": "",
                    "notifications_url": "",
                    "public_note": "",
                    "private_note": "",
                    "secret_entropy": "",
                    "evm_public_address": "",
                    "icp_principal": "6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                    "seed_phrase": "",
                    "from_placeholder_user_id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                    "redeem_code": "RedeemTokenID_e36dad15-f770-456a-b935-a4048cdc6cfd",
                    "created_at": 1756124757887,
                    "last_online_ms": 0,
                    "external_id": null,
                    "external_payload": null
                }
            },
            "CONTACTS_BY_ICP_PRINCIPAL_HASHTABLE": {
                "3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae"
            },
            "CONTACTS_BY_TIME_LIST": [
                "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae"
            ],
            "HISTORY_SUPERSWAP_USERID": {},
            "folder_uuid_to_metadata": {
                "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a": {
                    "id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "name": "",
                    "parent_folder_id": null,
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755588857475,
                    "subfolder_uuids": "[\"FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220\",\"FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a\"]",
                    "file_uuids": "[\"FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa\"]",
                    "last_updated_date_ms": 1755588857475,
                    "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET",
                    "deleted": 0,
                    "expires_at": -1,
                    "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "restore_trash_prior_folder_uuid": null,
                    "has_sovereign_permissions": 1,
                    "shortcut_to": null,
                    "notes": null,
                    "external_id": null,
                    "external_payload": null
                },
                "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4": {
                    "id": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                    "name": ".trash",
                    "parent_folder_id": null,
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755588857475,
                    "subfolder_uuids": "[]",
                    "file_uuids": "[]",
                    "last_updated_date_ms": 1755588857475,
                    "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET",
                    "deleted": 0,
                    "expires_at": -1,
                    "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "restore_trash_prior_folder_uuid": null,
                    "has_sovereign_permissions": 1,
                    "shortcut_to": null,
                    "notes": null,
                    "external_id": null,
                    "external_payload": null
                },
                "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220": {
                    "id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
                    "name": "mine aws",
                    "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/mine aws/",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755588916504,
                    "subfolder_uuids": "[]",
                    "file_uuids": "[\"FileID_af475a5a-6699-4f37-9305-22d96ca09111\"]",
                    "last_updated_date_ms": 1755588938944,
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
                    "external_payload": null
                },
                "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a": {
                    "id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                    "name": "Revised Investigation (2) (2)",
                    "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2) (2)/",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755590718251,
                    "subfolder_uuids": "[]",
                    "file_uuids": "[]",
                    "last_updated_date_ms": 1755592454756,
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
                    "external_payload": null
                },
                "FolderID_7403fbbf-3cac-486f-8d93-80d6eed8bcbf": {
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
                    "external_payload": null
                }
            },
            "file_uuid_to_metadata": {
                "FileID_af475a5a-6699-4f37-9305-22d96ca09111": {
                    "id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
                    "name": "Revised Proposal",
                    "parent_folder_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "version_id": "FileVersionID_2bfa2c8a-2ecd-42c3-a157-65d7e48ad103",
                    "extension": "jpeg",
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Proposal",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755589485206,
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET",
                    "file_size": 11242,
                    "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_af475a5a-6699-4f37-9305-22d96ca09111.jpeg",
                    "last_updated_date_ms": 1755935916460,
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
                    "external_payload": ""
                },
                "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa": {
                    "id": "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa",
                    "name": "Revised Proposal",
                    "parent_folder_id": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                    "version_id": "FileVersionID_13ca3558-c1e3-4f0c-983e-b086cf95a55e",
                    "extension": "Proposal",
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/Revised Proposal",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755590323356,
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET",
                    "file_size": 124434,
                    "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa.Proposal",
                    "last_updated_date_ms": 1755590897618,
                    "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "deleted": 1,
                    "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "upload_status": "QUEUED",
                    "expires_at": -1,
                    "restore_trash_prior_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "has_sovereign_permissions": 0,
                    "shortcut_to": null,
                    "notes": "",
                    "external_id": "",
                    "external_payload": ""
                },
                "FileID_a98bfde3-5edf-48de-b774-29285208d1cb": {
                    "id": "FileID_a98bfde3-5edf-48de-b774-29285208d1cb",
                    "name": "download.jpeg",
                    "parent_folder_id": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                    "version_id": "FileVersionID_ecc638b6-95dd-4960-ab41-44588dbd953b",
                    "extension": "jpeg",
                    "full_directory_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/download.jpeg",
                    "created_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "created_at": 1755591693465,
                    "disk_id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "disk_type": "AWS_BUCKET",
                    "file_size": 11242,
                    "raw_url": "https://officex.otterpad.cc/v1/drive/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae/directory/asset/FileID_a98bfde3-5edf-48de-b774-29285208d1cb.jpeg",
                    "last_updated_date_ms": 1755591693465,
                    "last_updated_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "deleted": 1,
                    "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "upload_status": "COMPLETED",
                    "expires_at": -1,
                    "restore_trash_prior_folder_uuid": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "has_sovereign_permissions": 0,
                    "shortcut_to": null,
                    "notes": "",
                    "external_id": "",
                    "external_payload": ""
                }
            },
            "full_folder_path_to_uuid": {
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/mine aws/": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2) (2)/": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation/": "FolderID_7403fbbf-3cac-486f-8d93-80d6eed8bcbf"
            },
            "full_file_path_to_uuid": {
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Proposal": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/Revised Proposal": "FileID_b2705f0d-9faa-476e-84b4-b0bacaa333aa",
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/download.jpeg": "FileID_a98bfde3-5edf-48de-b774-29285208d1cb"
            },
            "DISKS_BY_ID_HASHTABLE": {
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939": {
                    "id": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939",
                    "name": "Amazon Storage Generic Vendor",
                    "disk_type": "AWS_BUCKET",
                    "private_note": "Redeemed from gift card, claimed by UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "public_note": "Amazon S3 Storage Giftcard from \"Generic Vendor\"",
                    "auth_json": "{\"endpoint\":\"https://s3.amazonaws.com\",\"access_key\":\"AKIAXRT2PYYNLCFMDDO6\",\"secret_key\":\"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\",\"bucket\":\"officex-customerpurchaseid-92b68f13-93f3-4856-9283-d0f908b5c633\",\"region\":\"us-east-1\"}",
                    "created_at": 1755588857475,
                    "root_folder": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "trash_folder": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                    "external_id": null,
                    "external_payload": null,
                    "autoexpire_ms": null,
                    "billing_url": null
                }
            },
            "DISKS_BY_TIME_LIST": [
                "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939"
            ],
            "DRIVES_BY_ID_HASHTABLE": {
                "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae": {
                    "id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "name": "Anonymous Org",
                    "icp_principal": "cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "public_note": null,
                    "private_note": null,
                    "host_url": "https://officex.otterpad.cc",
                    "last_indexed_ms": null,
                    "created_at": 1755581408331,
                    "external_id": "",
                    "external_payload": null
                }
            },
            "DRIVES_BY_TIME_LIST": [
                "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae"
            ],
            "DIRECTORY_PERMISSIONS_BY_ID_HASHTABLE": {
                "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf": {
                    "id": "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf",
                    "resource_type": "Folder",
                    "resource_id": "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/",
                    "grantee_type": "Group",
                    "grantee_id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 1,
                    "note": "Default permissions for disk root folder owner",
                    "created_at": 1755588857475,
                    "last_modified_at": 1755588857475,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "DirectoryPermissionID_b5f7edfc-8e4b-4aa3-811f-faee4784e493": {
                    "id": "DirectoryPermissionID_b5f7edfc-8e4b-4aa3-811f-faee4784e493",
                    "resource_type": "Folder",
                    "resource_id": "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::.trash/",
                    "grantee_type": "Group",
                    "grantee_id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 0,
                    "note": "Default permissions for disk trash folder owner",
                    "created_at": 1755588857475,
                    "last_modified_at": 1755588857475,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a": {
                    "id": "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a",
                    "resource_type": "File",
                    "resource_id": "FileID_af475a5a-6699-4f37-9305-22d96ca09111",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Proposal",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 0,
                    "note": "",
                    "created_at": 1755613864580,
                    "last_modified_at": 1755613864580,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b": {
                    "id": "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b",
                    "resource_type": "Folder",
                    "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2) (2)/",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 0,
                    "note": "",
                    "created_at": 1755613909856,
                    "last_modified_at": 1755613909856,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37": {
                    "id": "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37",
                    "resource_type": "Folder",
                    "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2) (2)/",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 0,
                    "note": "Hello World",
                    "created_at": 1755614467277,
                    "last_modified_at": 1755614502476,
                    "redeem_code": null,
                    "from_placeholder_grantee": "PlaceholderPermissionGranteeID_08f6a75d-a5a8-4855-8d4a-00e79d386dd2",
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739": {
                    "id": "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739",
                    "resource_type": "Folder",
                    "resource_id": "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a",
                    "resource_path": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/Revised Investigation (2) (2)/",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 0,
                    "expiry_date_ms": -1,
                    "inheritable": 0,
                    "note": "Hello World",
                    "created_at": 1755614678534,
                    "last_modified_at": 1755614702963,
                    "redeem_code": null,
                    "from_placeholder_grantee": "PlaceholderPermissionGranteeID_7c7c2517-c7f7-4ae9-8448-701bc5feaedd",
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                }
            },
            "DIRECTORY_PERMISSIONS_BY_RESOURCE_HASHTABLE": {
                "FolderID_b44cfb98-2278-42d8-b846-c16f3c70da2a": [
                    "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf"
                ],
                "FolderID_10738639-5c2f-4fc8-a9cd-b5c3c3b3c6c4": [
                    "DirectoryPermissionID_b5f7edfc-8e4b-4aa3-811f-faee4784e493"
                ],
                "FileID_af475a5a-6699-4f37-9305-22d96ca09111": [
                    "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a"
                ],
                "FolderID_b9fa11bc-2926-4a13-944e-e1189df66e5a": [
                    "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b",
                    "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37",
                    "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739"
                ]
            },
            "DIRECTORY_GRANTEE_PERMISSIONS_HASHTABLE": {
                "undefined": [
                    "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf",
                    "DirectoryPermissionID_b5f7edfc-8e4b-4aa3-811f-faee4784e493",
                    "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a",
                    "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b",
                    "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37",
                    "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739"
                ]
            },
            "DIRECTORY_PERMISSIONS_BY_TIME_LIST": [
                "DirectoryPermissionID_3acdba66-1378-4257-bc9b-0563dd9c3bbf",
                "DirectoryPermissionID_b5f7edfc-8e4b-4aa3-811f-faee4784e493",
                "DirectoryPermissionID_93b6ff84-529d-4952-b89a-33f49beab44a",
                "DirectoryPermissionID_9591320e-e001-471e-8423-3dbd298bad2b",
                "DirectoryPermissionID_ccb14bfc-2aa1-40af-a5ec-01740f0b2f37",
                "DirectoryPermissionID_e7c84df4-2f4a-4de8-8598-ba3c125eb739"
            ],
            "SYSTEM_PERMISSIONS_BY_ID_HASHTABLE": {
                "SystemPermissionID_aa0c3f43-695d-4de3-994c-a06afa94da05": {
                    "id": "SystemPermissionID_aa0c3f43-695d-4de3-994c-a06afa94da05",
                    "resource_type": "Table",
                    "resource_identifier": "TABLE_DISKS",
                    "grantee_type": "Group",
                    "grantee_id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 1755581408331,
                    "expiry_date_ms": -1,
                    "note": "Allow 'Group for All' to view all disks by default.",
                    "created_at": 1755581408331,
                    "last_modified_at": 1755581408331,
                    "redeem_code": "REDEEM_1755581408331",
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591": {
                    "id": "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
                    "resource_type": "Table",
                    "resource_identifier": "TABLE_CONTACTS",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 1753290541568,
                    "expiry_date_ms": 0,
                    "note": "",
                    "created_at": 1755655944656,
                    "last_modified_at": 1755656836765,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                },
                "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7": {
                    "id": "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7",
                    "resource_type": "Table",
                    "resource_identifier": "TABLE_CONTACTS",
                    "grantee_type": "User",
                    "grantee_id": "UserID_wocat-vmb4r-rs5oj-ixung-f6e4c-r3zpk-ae2tm-jcmqr-vchpb-umcdf-fqe",
                    "granted_by": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "begin_date_ms": 1753290541568,
                    "expiry_date_ms": -1,
                    "note": "",
                    "created_at": 1755657381424,
                    "last_modified_at": 1755657381424,
                    "redeem_code": null,
                    "from_placeholder_grantee": null,
                    "metadata_type": null,
                    "metadata_content": null,
                    "external_id": null,
                    "external_payload": null
                }
            },
            "SYSTEM_PERMISSIONS_BY_RESOURCE_HASHTABLE": {
                "undefined": [
                    "SystemPermissionID_aa0c3f43-695d-4de3-994c-a06afa94da05",
                    "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
                    "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7"
                ]
            },
            "SYSTEM_GRANTEE_PERMISSIONS_HASHTABLE": {
                "undefined": [
                    "SystemPermissionID_aa0c3f43-695d-4de3-994c-a06afa94da05",
                    "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
                    "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7"
                ]
            },
            "SYSTEM_PERMISSIONS_BY_TIME_LIST": [
                "SystemPermissionID_aa0c3f43-695d-4de3-994c-a06afa94da05",
                "SystemPermissionID_8743dd9e-7f1a-457a-8560-b3c995da7591",
                "SystemPermissionID_b8367246-6d67-4f57-9e89-ec7b6d0f4bb7"
            ],
            "INVITES_BY_ID_HASHTABLE": {
                "GroupInviteID_2e42a943-e46f-401a-952e-4a9f6cddb4e9": {
                    "id": "GroupInviteID_2e42a943-e46f-401a-952e-4a9f6cddb4e9",
                    "group_id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "inviter_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "invitee_type": "USER",
                    "invitee_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "role": "ADMIN",
                    "note": "giftcard GiftcardSpawnOrgID_5df5d6cd-89d0-4f75-9d67-01f155af92bb was redeemed to spawn drive with 3500000000000 cycles, owned by UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae, on timestamp_ms 1755581408331 2025-08-19T05:30:08.331Z",
                    "active_from": 1755581408331,
                    "expires_at": -1,
                    "created_at": 1755581408331,
                    "last_modified_at": 1755581408331,
                    "redeem_code": "REDEEM_1755581408331",
                    "from_placeholder_invitee": null,
                    "external_id": null,
                    "external_payload": null
                },
                "GroupInviteID_d9e89f8e-eec3-4dd1-9c97-6c66c4ac779d": {
                    "id": "GroupInviteID_d9e89f8e-eec3-4dd1-9c97-6c66c4ac779d",
                    "group_id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "inviter_id": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "invitee_type": "USER",
                    "invitee_id": "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae",
                    "role": "MEMBER",
                    "note": "Auto-invited to default 'Group for All' upon contact creation.",
                    "active_from": 1756124757888,
                    "expires_at": -1,
                    "created_at": 1756124757888,
                    "last_modified_at": 1756124757888,
                    "redeem_code": null,
                    "from_placeholder_invitee": null,
                    "external_id": null,
                    "external_payload": null
                }
            },
            "USERS_INVITES_LIST_HASHTABLE": {
                "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae": [
                    "GroupInviteID_2e42a943-e46f-401a-952e-4a9f6cddb4e9"
                ],
                "UserID_6o5oj-gl42v-odqny-f3p5q-7deq3-iunwf-3osz3-m7aod-d43rx-su5ec-hae": [
                    "GroupInviteID_d9e89f8e-eec3-4dd1-9c97-6c66c4ac779d"
                ]
            },
            "GROUPS_BY_ID_HASHTABLE": {
                "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781": {
                    "id": "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781",
                    "name": "Group for All",
                    "owner": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
                    "avatar": null,
                    "public_note": null,
                    "private_note": null,
                    "created_at": 1755581408331,
                    "last_modified_at": 1755581408331,
                    "drive_id": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
                    "host_url": "https://officex.otterpad.cc",
                    "external_id": null,
                    "external_payload": null
                }
            },
            "GROUPS_BY_TIME_LIST": [
                "GroupID_1873ebab-1403-412d-99ea-41a5f0d0c781"
            ],
            "WEBHOOKS_BY_ALT_INDEX_HASHTABLE": {},
            "WEBHOOKS_BY_ID_HASHTABLE": {},
            "WEBHOOKS_BY_TIME_LIST": [],
            "PURCHASES_BY_ID_HASHTABLE": {
                "PurchaseID_32164a50-bf48-4d8d-9d13-a7fde18712db": {
                    "id": "PurchaseID_32164a50-bf48-4d8d-9d13-a7fde18712db",
                    "template_id": null,
                    "vendor_name": "Amazon",
                    "vendor_id": "UserID_rxswe-tad5k-qwjsz-ooo5e-5py3z-wttmo-kx2kp-anfj7-rx7mb-356v3-yae",
                    "status": "PAID",
                    "description": "Successful Purchase!",
                    "about_url": "https://vendorofficex.otterpad.cc/v1/dashboard/customer/?vendor_purchase_id=CustomerPurchaseID_92b68f13-93f3-4856-9283-d0f908b5c633&customer_billing_api_key=c5ffc000-861b-4966-b23e-c5a07f38550f",
                    "run_url": null,
                    "billing_url": "https://vendorofficex.otterpad.cc/v1/dashboard/customer/?vendor_purchase_id=CustomerPurchaseID_92b68f13-93f3-4856-9283-d0f908b5c633&customer_billing_api_key=c5ffc000-861b-4966-b23e-c5a07f38550f",
                    "support_url": "https://vendorofficex.otterpad.cc/v1/dashboard/customer/?vendor_purchase_id=CustomerPurchaseID_92b68f13-93f3-4856-9283-d0f908b5c633&customer_billing_api_key=c5ffc000-861b-4966-b23e-c5a07f38550f",
                    "delivery_url": "https://officex.app/org/current/redeem/disk-giftcard?redeem=eyJuYW1lIjoiQW1hem9uIFN0b3JhZ2UgR2VuZXJpYyBWZW5kb3IiLCJkaXNrX3R5cGUiOiJBV1NfQlVDS0VUIiwicHVibGljX25vdGUiOiJBbWF6b24gUzMgU3RvcmFnZSBHaWZ0Y2FyZCBmcm9tIFwiR2VuZXJpYyBWZW5kb3JcIiIsImF1dGhfanNvbiI6IntcImVuZHBvaW50XCI6XCJodHRwczovL3MzLmFtYXpvbmF3cy5jb21cIixcImFjY2Vzc19rZXlcIjpcIkFLSUFYUlQyUFlZTkxDRk1ERE82XCIsXCJzZWNyZXRfa2V5XCI6XCJtcmtxd3pVb0dSb1BVV0kyQ0R2SWgxSUpUSTUzSmU4bGp4M1BCNFVPXCIsXCJidWNrZXRcIjpcIm9mZmljZXgtY3VzdG9tZXJwdXJjaGFzZWlkLTkyYjY4ZjEzLTkzZjMtNDg1Ni05MjgzLWQwZjkwOGI1YzYzM1wiLFwicmVnaW9uXCI6XCJ1cy1lYXN0LTFcIn0iLCJlbmRwb2ludCI6Imh0dHBzOi8vdmVuZG9yb2ZmaWNleC5vdHRlcnBhZC5jYy92MS9kYXNoYm9hcmQvY3VzdG9tZXIifQ",
                    "verification_url": null,
                    "installation_url": null,
                    "title": "Amazon S3 Storage Giftcard | Base L2 Topup Wallet",
                    "subtitle": "Amazon S3 Storage Giftcard | Base L2 Topup Wallet",
                    "pricing": "$0.01/GB/month storage, $0.01/GB egress",
                    "next_delivery_date": null,
                    "vendor_notes": "Share giftcard with a friend: https://officex.app/org/current/redeem/disk-giftcard?redeem=eyJuYW1lIjoiQW1hem9uIFN0b3JhZ2UgR2VuZXJpYyBWZW5kb3IiLCJkaXNrX3R5cGUiOiJBV1NfQlVDS0VUIiwicHVibGljX25vdGUiOiJBbWF6b24gUzMgU3RvcmFnZSBHaWZ0Y2FyZCBmcm9tIFwiR2VuZXJpYyBWZW5kb3JcIiIsImF1dGhfanNvbiI6IntcImVuZHBvaW50XCI6XCJodHRwczovL3MzLmFtYXpvbmF3cy5jb21cIixcImFjY2Vzc19rZXlcIjpcIkFLSUFYUlQyUFlZTkxDRk1ERE82XCIsXCJzZWNyZXRfa2V5XCI6XCJtcmtxd3pVb0dSb1BVV0kyQ0R2SWgxSUpUSTUzSmU4bGp4M1BCNFVPXCIsXCJidWNrZXRcIjpcIm9mZmljZXgtY3VzdG9tZXJwdXJjaGFzZWlkLTkyYjY4ZjEzLTkzZjMtNDg1Ni05MjgzLWQwZjkwOGI1YzYzM1wiLFwicmVnaW9uXCI6XCJ1cy1lYXN0LTFcIn0iLCJlbmRwb2ludCI6Imh0dHBzOi8vdmVuZG9yb2ZmaWNleC5vdHRlcnBhZC5jYy92MS9kYXNoYm9hcmQvY3VzdG9tZXIifQ",
                    "notes": "From checkout init route https://vendorofficex.otterpad.cc/v1/checkout/initiate with checkout session id CheckoutSessionID_66ef2f94-dbe6-4a9d-b757-4ea9f855c147",
                    "created_at": 1755588845956,
                    "updated_at": 1755588845956,
                    "last_updated_at": 1755588845956,
                    "tracer": "TracerID_449b35f9-8c86-4b5b-a703-72cf0e171ce9",
                    "external_id": null,
                    "external_payload": null
                }
            },
            "PURCHASES_BY_TIME_LIST": [
                "PurchaseID_32164a50-bf48-4d8d-9d13-a7fde18712db"
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

***

## Search Drive

Search within drives

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/organization/search
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/kwfgyjt/drive-org-id-organization-search?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| <p><br>query <mark style="color:red;">(required)</mark></p> | <p><strong>string &#x3C;= 256 characters</strong><br>Search query</p>                                                                                                  | mine aws    |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| categories                                                  | <p><strong>Array of strings</strong><br>Items Enum: "<strong>FILES</strong>" "<strong>FOLDERS</strong>" "<strong>METADATA</strong>"<br>Categories to search in</p>     | FOLDERS     |
| page\_size                                                  | <p><strong>integer [ 1 .. 1000 ]</strong><br>Default: 50<br>Number of items per page</p>                                                                               | 50          |
| cursor\_up                                                  | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (previous page)</p>                                                                 | string      |
| cursor\_down                                                | <p><strong>string or null &#x3C;= 256 characters</strong><br>Cursor for pagination (next page)</p>                                                                     | string      |
| sort\_by                                                    | <p><strong>string</strong> </p><p>Default: "<strong>UPDATED_AT</strong>" Enum: "<strong>CREATED_AT</strong>" "<strong>UPDATED_AT</strong>" </p><p>Field to sort by</p> | CREATED\_AT |
| direction                                                   | <p><strong>string</strong></p><p>Default: "ASC"</p><p>Enum: "ASC" "DESC"</p><p>Sort direction</p>                                                                      | ASC         |



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
                    "resource_id": "FolderID_2042047e-b6ec-4306-9b33-f8ad6afcf220",
                    "title": "mine aws",
                    "preview": "DiskID_d2b1fec9-ebf8-4ca5-adb3-8dea93941939::/mine aws/",
                    "score": -6.414495796693654,
                    "category": "FOLDERS",
                    "metadata": null,
                    "created_at": 1755588916504,
                    "updated_at": 1755588938944
                }
            ],
            "page_size": 20,
            "total": 1,
            "direction": "DESC"
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
| Request  | [IRequestSearchDrive](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L620)  |
| Response | [IResponseSearchDrive](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L636) |

***

## Get Current User Info

Get information about the current authenticated user

<mark style="color:green;background-color:green;">GET</mark> &#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/organization/whoami
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/o4ddkqt/drive-org-id-organization-whoami?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

<details>

<summary>P<strong>ath Parameter</strong></summary>

| organization\_id <mark style="color:red;">(required)</mark> | <p><strong>string (DriveID)</strong></p><p>Unique identifier for a drive</p> | DriveID\_abc123 |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | --------------- |

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
            "nickname": "Owner",
            "userID": "UserID_3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "driveID": "DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae",
            "icp_principal": "3hrnt-ylswl-acoxp-fx4qh-irpw4-wyyx5-pdjfq-ih5cl-d2xy3-dfbga-tae",
            "evm_public_address": "",
            "is_owner": true,
            "drive_nickname": "Anonymous Org"
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

|          | type                                                                                                                           |
| -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Response | [IResponseWhoAmI](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1472) |

***

## Shortlinks

Built-in url shortener for filesharing convenience

<mark style="color:blue;background-color:blue;">POST</mark>&#x20;

```url
https://dev.officex.app/v1/drive/{organization_id}/organization/shortlink
```

<a href="https://www.postman.com/officexapp-3755884/official-officex-public-rest-api/request/fuotu6f/drive-org-id-organization-shortlink-create?action=share&#x26;source=copy-link&#x26;creator=47657005" class="button primary">Run In Postman</a>

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

| <p><br>original_url <mark style="color:red;">(required)</mark></p> | <p><strong>string</strong><br>original url  </p> | [https://google.com/my-final-destination](https://google.com/my-final-destination) |
| ------------------------------------------------------------------ | ------------------------------------------------ | ---------------------------------------------------------------------------------- |



</details>

#### Responses

<details>

<summary><mark style="color:$success;">success</mark></summary>

```json
{
    "ok": {
        "data": {
            "slug": "1f673c0f-0d36-4ce6-9515-7e05450f5479",
            "original_url": "https://google.com/my-final-destination",
            "shortlink_url": "https://officex.app/org/DriveID_cvdg6-kpgru-3fohl-znr3p-dx3gg-em3qk-qyqoy-gqdrk-wg7n2-ufa4d-bae__aHR0cHM6Ly9vZmZpY2V4Lm90dGVycGFkLmNj/to/1f673c0f-0d36-4ce6-9515-7e05450f5479"
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
| Request  | [IRequestShortLink](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1803)  |
| Response | [IResponseShortLink](https://github.com/OfficeXApp/types/blob/42f029085e56fb3f321f1d51962d09f939f85d77/src/types/routes.ts#L1808) |
