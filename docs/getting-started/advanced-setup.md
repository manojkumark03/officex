---
description: Multi-Stage Deployments for Granular Control
---

# Advanced Setup

While the [2 min quickstart](../) is sufficient for most integrations, some companies may want more granular control and security around user custody and how those identities are created.

For example, you are a Discord clone that wants to provide anon workspaces for your users. You have 10,000 "communities" with members, each of whom are a "user", and users can belong to many communities. In total you have 1M users.

This Advanced Setup Guide will show how to run a fully custom setup. This method is mandatory if you are running OfficeX servers on a trustless decentralized web3 cloud (ICP canisters).

### Create New Organization

The advanced process outline:

{% stepper %}
{% step %}
### Create Your Admin Identity

Users in OfficeX are merely crypto wallets, which we can generate offline.
{% endstep %}

{% step %}
### Create Factory Giftcard

Imagine OfficeX as a vending machine factory that spawns workspaces, purchased with free giftcards. Create as many free giftcards as you like.
{% endstep %}

{% step %}
### Redeem Factory Giftcard

Pay the vending machine with your free giftcard. It will deploy your new workspace inside an encrypted multi-tenant web2 linux server or to the blockchain as a web3 server (ICP canister)
{% endstep %}

{% step %}
### Activate Workspace

Your anon workspace is deployed and blank, waiting for you to activate it. This is the final step, welcome home.
{% endstep %}
{% endstepper %}

Let's dive into it step by step:

<details>

<summary><code>Step 1</code> Create Your Admin Identity</summary>

Users in OfficeX are merely crypto wallets. Let's create them!

There are three ways to create your admin identity:

1. Self Custody External ICP wallet (Internet Computer wallet such as [Plug Wallet](https://plugwallet.ooo/), [OISY Wallet](https://oisy.com/))
2. Convenience cloud route `/generate-crypto-identity`&#x20;
3. Offline using your own code (most securely scaleable)

We recommend using Option #2 of `/generate-crypto-identity` as its the easiest. Understand the tradeoffs below. We also recommend reading the [Authentication Guide](../core-concepts/authentication.md).



`Option #1 - Self Custody External ICP Wallet`     &#x20;

Choose this option if you want to use a multi-sig as the superadmin owner of the workspace. This is particularly useful if you are a DAO (decentralized autonomous organization).&#x20;

```
1. Download your ICP wallet and copy the principal id of your wallet
2. Append `UserID_` to it, and its now a valid OfficeX UserID

For example:
const principal_id = "b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae";
const officex_user_id = `UserID_${principal_id}`

console.log(officex_user_id)
// returns "UserID_b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae"
```

Now you can use this user id as your admin, in the subsequent future steps.

\
\
`Option #2 - Convenience cloud route /generate-crypto-identity`&#x20;

Choose this option if you want convinence. Our free public cloud will handle creating the user. Beware of unofficial servers that may log your generated crypto identities. While those crypto wallets are not used to hold money, they can sign 30 second auth tokens to interact with REST API on your behalf. Read the [Authentication Guide](../core-concepts/authentication.md) to learn more.&#x20;

Only trust servers from the domain `officex.app` or `anonwork.space` , for example, `https://us-east-1.officex.app` or `https://ap-northeast-1.anonwork.space` . We maintain a list of valid domains in the [Authentication Guide](../core-concepts/authentication.md).&#x20;

The `secret_entropy` can be any string, often a concatenation of your database user id plus some secret string. It will lead to the same deterministic user generated every time.

The `seed_phrase` , if you choose to use this method, must be a valid BIP-39 Mnemonic Seed from [this wordlist.](https://www.blockplate.com/pages/bip-39-wordlist) Both methods are valid, we recommend using `secret_entropy` as its flexibly adaptable to your existing user ids.

```typescript
import { IRequestGenerateCryptoIdentity } from "officexapp/types"

const payload: IRequestGenerateCryptoIdentity = {
    secret_entropy?: string;
    seed_phrase?: string;
};

const admin: IResponseGenerateCryptoIdentity = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/helpers/generate-crypto-identity`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseGenerateCryptoIdentity {
  user_id: UserID; // only the user_id is needed for subsequent steps
  icp_principal: string;
  evm_public_key: string;
  evm_private_key: string;
  origin: {
    secret_entropy?: string;
    seed_phrase?: string;
  };
}
```



`Option #3 - Offline using your own code`

Choose this option if you want to maintain a high bar of security over custodial users while using 3rd party servers. It is simply running the same code that powers Option #2 `/generate-crypto-identity` , except on your own offline servers. You can see proof of this by testing the same `secret_entropy` string in both.

<a href="https://codesandbox.io/p/sandbox/generate-crypto-identities-officex-sn95h3" class="button primary" data-icon="terminal">Run in Codepen</a>

```typescript
import { wordlist } from "@scure/bip39/wordlists/english";
import { generateMnemonic } from "@scure/bip39";
import { Ed25519KeyIdentity } from "@dfinity/identity";
import { mnemonicToAccount } from "viem/accounts";
import { bytesToHex, sha256, toBytes } from "viem";
import * as bip39 from "bip39";
import { mnemonicToSeedSync } from "@scure/bip39";
import {
  IRequestGenerateCryptoIdentity,
  IDPrefixEnum,
  UserID,
} from "@officexapp/types";

export const generateCryptoIdentity = async (
  args: IRequestGenerateCryptoIdentity
): Promise<{
  user_id: UserID;
  icp_principal: string;
  evm_public_key: string;
  evm_private_key: string;
  origin: {
    secret_entropy?: string;
    seed_phrase?: string;
  };
}> => {
  const { secret_entropy, seed_phrase } = args;

  if (!secret_entropy && !seed_phrase) {
    // create a user completely from scratch
    const seed = generateRandomSeed();
    const wallets = await seed_phrase_to_wallet_addresses(seed);

    const cryptoIdentity = {
      user_id: `${IDPrefixEnum.User}${wallets.icp_principal}`,
      icp_principal: wallets.icp_principal,
      evm_public_key: wallets.evm_public_address,
      evm_private_key: wallets.evm_private_key,
      origin: {
        secret_entropy,
        seed_phrase,
      },
    };

    return cryptoIdentity;
  } else if (seed_phrase) {
    const wallets = await seed_phrase_to_wallet_addresses(seed_phrase);
    const cryptoIdentity = {
      user_id: `${IDPrefixEnum.User}${wallets.icp_principal}`,
      icp_principal: wallets.icp_principal,
      evm_public_key: wallets.evm_public_address,
      evm_private_key: wallets.evm_private_key,
      origin: {
        secret_entropy,
        seed_phrase,
      },
    };
    return cryptoIdentity;
  } else if (secret_entropy) {
    const seed = passwordToSeedPhrase(secret_entropy);
    const wallets = await seed_phrase_to_wallet_addresses(seed);
    const cryptoIdentity = {
      user_id: `${IDPrefixEnum.User}${wallets.icp_principal}`,
      icp_principal: wallets.icp_principal,
      evm_public_key: wallets.evm_public_address,
      evm_private_key: wallets.evm_private_key,
      origin: {
        secret_entropy,
        seed_phrase,
      },
    };
    return cryptoIdentity;
  } else {
    throw new Error("Invalid arguments");
  }
};

// Helper function to generate a random seed phrase
const generateRandomSeed = (): string => {
  // return (generate(12) as string[]).join(" ");
  return generateMnemonic(wordlist, 128);
};

const seed_phrase_to_wallet_addresses = async (seedPhrase: string) => {
  try {
    // For EVM address generation
    const evmAccount = mnemonicToAccount(seedPhrase);
    const evmAddress = evmAccount.address;

    const derivedKey = await deriveEd25519KeyFromSeed(
      mnemonicToSeedSync(seedPhrase || "")
    );
    // Create the identity from the derived key
    // @ts-ignore
    const identity = Ed25519KeyIdentity.fromSecretKey(derivedKey);

    // Get the principal using the identity's getPrincipal method
    const principal = identity.getPrincipal();
    const principalStr = principal.toString();

    return {
      icp_principal: principalStr,
      evm_public_address: evmAddress,
      // @ts-ignore
      evm_private_key: bytesToHex(evmAccount.getHdKey().privateKey),
      seed_phrase: seedPhrase,
    };
  } catch (error) {
    console.error("Failed to generate addresses:", error);
    throw error;
  }
};

const passwordToSeedPhrase = (password: string) => {
  // 1. Generate a deterministic hash (entropy) from the password.
  const passwordBytes = new TextEncoder().encode(password);

  // The sha256 function from viem returns a hex string.
  const entropyHex = sha256(passwordBytes);

  // 2. Convert the hex string to a Uint8Array using viem's toBytes function.
  const entropyBytes = toBytes(entropyHex);

  // 3. Use bip39.entropyToMnemonic to convert the entropy into a mnemonic.
  // The library expects a Buffer, so we need to convert our Uint8Array.
  return bip39.entropyToMnemonic(Buffer.from(entropyBytes), wordlist);
};

// Function to derive Ed25519 key from seed (uses the first 32 bytes of the seed)
const deriveEd25519KeyFromSeed = async (
  seed: Uint8Array
): Promise<Uint8Array> => {
  const hashBuffer = await crypto.subtle.digest("SHA-256", seed);
  return new Uint8Array(hashBuffer).slice(0, 32); // Ed25519 secret key should be 32 bytes
};

```

</details>

<details>

<summary><code>Step 2</code> Create Factory Giftcard</summary>

Imagine OfficeX as a vending machine factory that spawns workspaces, purchased with free giftcards. Create as many free giftcards as you like, on our free public cloud.&#x20;

Note that if you are running OfficeX on a trustless decentralized web3 cloud (ICP canisters), giftcards are not free as deployment of smart contracts cost crypto for gas. Find a vendor selling giftcards in the [Vendor Marketplace.](../core-concepts/vendor-marketplace.md)



<a href="https://codesandbox.io/p/sandbox/bulk-scripting-officex-554k66" class="button primary" data-icon="terminal">Run in Codepen</a>

```typescript
import { IRequestCreateGiftcardSpawnOrg, BundleDefaultDisk, IResponseCreateGiftcardSpawnOrg, GiftcardSpawnOrgID } from "officexapp/types"

const payload: IRequestCreateGiftcardSpawnOrg = {
    usd_revenue_cents?: number;
    note?: string;
    gas_cycles_included?: number;
    external_id?: string;
    bundled_default_disk?: BundleDefaultDisk;
}

const admin: IResponseCreateGiftcardSpawnOrg = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/giftcards/spawnorg/create`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseCreateGiftcardSpawnOrg {
  id: GiftcardSpawnOrgID; // string
  usd_revenue_cents: number;
  note: string;
  gas_cycles_included: number;
  timestamp_ms: number;
  external_id?: string;
  redeemed: boolean;
  bundled_default_disk?: BundleDefaultDisk;
}
```

Great! All you need is to keep the `GiftcardSpawnOrgID` to use in subsequent steps.

</details>

<details>

<summary><code>Step 3</code> Redeem Factory Giftcard</summary>

Now that you have a `GiftcardSpawnOrgID` and admin `UserID` , we can redeem the factory giftcard and receive a fresh new workspace, deployed from the "vending machine".

<a href="https://codesandbox.io/p/sandbox/bulk-scripting-officex-554k66" class="button primary" data-icon="terminal">Run in Codepen</a>&#x20;

```typescript
import { IRequestRedeemGiftcardSpawnOrg, IResponseRedeemGiftcardSpawnOrg, GiftcardSpawnOrgID, UserID, DriveID } from "officexapp/types"

const payload: IRequestRedeemGiftcardSpawnOrg = {
    giftcard_id: GiftcardSpawnOrgID;
    owner_user_id: UserID;
    owner_name?: string;
    organization_name?: string;
    external_id?: string;
    email?: string;
}

const admin: IResponseRedeemGiftcardSpawnOrg = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/giftcards/spawnorg/redeem`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseRedeemGiftcardSpawnOrg {
    owner_id: UserID;
    drive_id: DriveID;
    host: string;
    redeem_code: string; // important: do not expose this secret
    external_id?: string;
}
```

Hold on to that returned `redeem_code` as we need it for the final step (activating our workspace). We also need the returned `host` and `DriveID` (aka organization id).

Be careful not to lose it as anyone can use it to activate the org and login as admin with default api keys. Note that this is by design, as sometimes the superadmin owner is a infrequent use multi-sig, which is why we decouple the workspace activation. The owner superadmin wallet is able to deactivate lost api keys via signature auth. Learn more in the [Authentication Guide.](../core-concepts/authentication.md)

</details>

<details>

<summary><code>Step 4</code> Activate Workspace</summary>

Finally, we can use the `redeem_code` to activate our new workspace. This just creates an admin api key, deploys any default storage disks, and provides a convenient auto-login url for browsers.

Note that the `host` and `DriveID` strings are also needed to query the right backend server. These were returned to you in the previous step `Redeem Factory Giftcard`.

<a href="https://codesandbox.io/p/sandbox/bulk-scripting-officex-554k66" class="button primary" data-icon="terminal">Run in Codepen</a>

```typescript
import { IRequestRedeemOrg, IResponseRedeemOrg, GiftcardSpawnOrgID, UserID, DriveID } from "officexapp/types"

const payload: IRequestRedeemOrg {
    redeem_code: string;
}

const admin: IResponseRedeemOrg = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/redeem`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseRedeemOrg {
    note: string;
    drive_id: DriveID;
    host_url: string;
    api_key: string; // use this in future REST API call
    auto_login_url: string; // use this to login in browser
}
```

We are finished! Now you can use the `auto_login_url` to open OfficeX on web browser and auto login as owner superadmin. You can also use the `api_key` to interact with the REST API on behalf of owner superadmin. Be sure to save these variables to your own database for easy future reference.

For sanity check, we can query the organizations `/whoami` endpoint with `api_key` to verify its working.

```typescript
import { IResponseWhoAmI, DriveID } from "officexapp/types"

const admin: IResponseWhoAmI = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/whoami`, {
      method: "GET",
      headers: { 
          "Content-Type": "application/json",
          "Authorization": `Bearer ${api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseWhoAmI {
    driveID: DriveID;
    drive_nickname: string;
    evm_public_address: string;
    icp_principal: string;
    is_owner: boolean;
    nickname: string;
    userID: UserID;
}
```

Congratulations on creating your new OfficeX Anonymous Workspace!&#x20;

Next Steps? Check out the [REST API reference](https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/XdQ7dOsfwiLPSkHYfPSw/) to see how to create contacts, join groups, create permits & more!

</details>



### Create New User

In our example, users can belong to many organizations. While the previous script created new organizations along with their admin user, not every user will be an admin. So we must run another process for those users.

The advanced process outline:

{% stepper %}
{% step %}
### Create Crypto Identity

Users in OfficeX are merely crypto wallets, which we can generate offline.
{% endstep %}

{% step %}
### Create API Key (optional)

Create API Keys per org + user combo. This can be done in bulk or on-the-fly.
{% endstep %}

{% step %}
### Create Auto-Login URL (optional)

Get a simple auto-login url you can give users to visit in browser. Also can be done in bulk or on-the-fly. Not necessary if you are primarily using iframes UX within your own app.
{% endstep %}
{% endstepper %}

Let's dive into it step by step:

<details>

<summary><code>Step 1</code> Create Crypto Identity</summary>

This is the same process as shown in [Create Admin Identity.](https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/~/changes/26/getting-started/advanced-setup#create-new-organization) For brevity, please look there for code documentation and explanations.

Save the OfficeX `UserID` to your own database for each reference.

</details>

<details>

<summary><code>Step 2</code> Create API Key (optional)</summary>

Every unique combo of organization + user has its own "user api key for that organization". It is a many to many relationship. It is up to you to decide how to want to model that relationship in your own database. Likely you already have a join table, such as in our example "Discord Clone" where users can belong to many communities.

Here is how we can create an API Key for a user in an organization. You will need to either use the admin api key to do this, or alternatively allow contacts to generate their own api keys using [temporary auth signatures](https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/~/changes/26/core-concepts/authentication#temporary-auth-signatures). We recommend just using the organization admin api key.

First we must add the user to the organization as a contact. Only contacts can have API Keys. Users can still interact with orgs without api keys simply by using [temporary auth signatures](https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/~/changes/26/core-concepts/authentication#temporary-auth-signatures), but for persistence and convenience, we recommend using api keys (the availability of that temp auth flow is why this step is technically optional).

<a href="https://codesandbox.io/p/sandbox/bulk-scripting-officex-554k66" class="button primary" data-icon="terminal">Run in Codepen</a>



`Step 1 - Create Contact`

```typescript
import { IRequestCreateContact, IResponseCreateContact } from "officexapp/types"

const payload: IRequestCreateContact = {
    id: UserID;
    name: string;
    // ...other attributes optional
}

const contact: IResponseCreateContact = await (
    await fetch(`${host}/v1/drive/${DriveID}/contacts/create`, {
      method: "POST",
      headers: { 
          "Content-Type": "application/json",
          "Authorization": `Bearer ${admin_api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseCreateContact {
    id: UserID;
    // ...other attributes of type ContactFE
}
```

`Step 2 - Create API Key`

```typescript
import { IRequestCreateApiKey, IResponseCreateApiKey, UserID, ApiKeyID, DriveID } from "officexapp/types"

const payload: IRequestCreateApiKey = {
    name: string;
    user_id: UserID;
    begins_at?: number; // unix timestamp. 0 for immediately
    expires_at?: number; // unix timestamp. -1 for never expires
    // ...other attributes optional
}

const user_api_key_for_org: IResponseCreateApiKey = await (
    await fetch(`${host}/v1/drive/${DriveID}/api_keys/create`, {
      method: "POST",
      headers: {  
           "Content-Type": "application/json",
           "Authorization": `Bearer ${admin_api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseCreateApiKey {
  id: ApiKeyID;
  value: string; // the api key we can now use
  user_id: UserID;
  // ...other attributes of type ApiKeyFE
}
```

Great! Now you now have an api key representing your user in that organization. Save it to your database for easy future reference.

If you are using iframes to embed OfficeX into your app, this api key is all you need. If you are not using iframes and instead want to let users go to OfficeX directly in their web browser, proceed to the final `Step 3` to create auto-login urls for them.

</details>

<details>

<summary><code>Step 3</code> Create Auto-Login URLs (optional)</summary>

Auto-Login URLs are convenient if you want to let your users visit OfficeX directly in their web browser. This also saves you work if you don't want to use iframes.&#x20;

The below code uses the helper route `/generate-auto-login-link` but its merely a string manipulation wrapper and thus can also be done offline yourself by copying the same backend code [seen on Github.](https://github.com/OfficeXApp/typescript-server/blob/79c032cc721b31125d0272d6385b725296565b40/src/routes/v1/drive/contacts/handlers.ts#L1442)

<a href="https://codesandbox.io/p/sandbox/bulk-scripting-officex-554k66" class="button primary" data-icon="terminal">Run in Codepen</a>

```typescript
import { IRequestAutoLoginLink, IResponseAutoLoginLink, UserID, DriveID } from "officexapp/types"

const payload: IRequestAutoLoginLink = {
  user_id: UserID;
  profile_api_key: string;
}

const user_api_key_for_org: IResponseAutoLoginLink = await (
    await fetch(`${host}/v1/drive/${DriveID}/contacts/helpers/generate-auto-login-link`, {
      method: "POST",
      headers: {  
           "Content-Type": "application/json",
           "Authorization": `Bearer ${api_key}` // this is the users api key not the admin
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseAutoLoginLink {
  user_id: UserID;
  auto_login_link: string; // give users this url to open in web browser
  full_login_instructions: string;
}
```

That is all! Now your users can sign in directly to OfficeX on their web browser, into your designated organization and profile.

</details>





### Bulk Provision Workspaces for 1M users&#x20;

In our example, we are "Discord Clone" with 10k communities and 1 million users. What is the best way to bulk provision workspaces for them?

If you are using our free public cloud, its very easy just run a `for loop` script. If you are self hosting, the process is the same but you should read our docs on [Self Hosting](../core-concepts/public-cloud-vs-self-hosting.md) and [Performance Benchmarks](../codebase-explained/performance-benchmarks.md).

Here is what the bulk provisioning script looks like in `pseudo-code` (ie. the code is not real, just an explainer. scroll down to see the actual real code)

```typescript
// bulk_provision_script.ts

// written in pseudocode
for (const community of batch_communities) {
  // step 1. run the quickstarts
  const logins = await fetch("/quickstart")
  // step 2. save IDs to database
  const row = await updateDatabase(community, logins)
  // step 3. render as iframes for frontend
  const { iframe_url, auth_json } = row
}
```

`For each in loop`:

{% stepper %}
{% step %}
### Run the Quickstart&#x20;

Create a workspace for each community, including admin
{% endstep %}

{% step %}
### Save IDs to your database

Match org to org, user to user, and possibly api keys join table
{% endstep %}

{% step %}
### Render iFrames on Frontend

Using either api keys or deterministic&#x20;
{% endstep %}
{% endstepper %}

Let's dive into it step by step, looking at the `actual real code`.&#x20;

<details>

<summary><code>Step 1</code> Run the Quickstart</summary>

First we create the organization and decide an admin

```typescript
import { IRequestQuickstart, IResponseQuickstart } from "officexapp/types"

const quickstart: IRequestQuickstart = {
  org_name: "Adams Discord Community",
  tracer: "DiscordOrgID_123",
  admin: { 
    name: "Adam", 
    secret_entropy: `${"DiscordUserID_123"}_SECRET`, 
    tracer: "DiscordUserID_123" 
  },
  members: [
    { 
      name: "Benjamin",
      secret_entropy: `${"DiscordUserID_456"}_${MY_SECRET}`,
      tracer: "DiscordUserID_456" 
    }
  ]
}

const logins: IResponseQuickstart = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/quickstart`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(quickstart),
    })
  ).json();
  

const logins: IResponseQuickstart = {
  organization: {
    drive_id: "DriveID_sx6t2-bwmyg-34dko-jghjx-cxwkv-ucsa3-vkm53-6zppl-fxm6u-swo4d-mqe"
    org_name: "Adams Discord Community",
    host_url: "https://officex.otterpad.cc",
    frontend_url: "https://officex.app/org/DriveID_sx6t2-bwmyg-34dko-jghjx-cxwkv-ucsa3-vkm53-6zppl-fxm6u-swo4d-mqe__aHR0cHM6Ly9vZmZpY2V4Lm90dGVycGFkLmNj",
    tracer: "DiscordOrgID_123"
  },
  admin: {
    user_id: "UserID_gbu2g-lduz2-mlo7z-gpkac-jytn3-tqh24-pj2hb-5zjw4-x5va6-dfb5y-yae",
    api_key_value: "API_KEY_FOR_UserID_gbu"
    auto_login_url: "https://officex.app/auto-login?token=eyJvcm...",
    auth_json: IFrameInjectedAuth;
    tracer: "DiscordUserID_123"
  },
  members: [{
    user_id: "UserID_q3tec-umjm4-kl7jk-zwi6l-7hjj4-7m7ba-xprr7-kur7x-c2mv2-lub65-2qe",
    api_key_value: "API_KEY_FOR_UserID_q3t",
    auto_login_url: "https://officex.app/auto-login?token=ad4vcm...",
    auth_json: IFrameInjectedAuth;
    tracer: "DiscordUserID_456"
  }]
}
```



</details>

<details>

<summary><code>Step 2</code> Save IDs to your database</summary>

Then we save the generated officex organization & user credentials, to your own database solution.&#x20;

```typescript
// continuing on from prior step code
const MY_ORG_ID = "DiscordOrgID_123"
const MY_USER_ID = "DiscordUserID_456"

await updateDatabase(MY_ORG_ID, logins)
await updateDatabase(`${MY_ORG_ID}_${MY_USER_ID}`, member.api_key_value)
```

</details>

<details>

<summary><code>Step 3</code> Render iFrames on Frontend</summary>

For the purpose of this demo, we will choose to send api keys to frontend iframe for every attempt of a user navigating to workspace. Simply provide up-to-date `IFrameInjectedConfig` to client devices.&#x20;

```typescript
// continuing on from prior step code
import { IFrameInjectedConfig } from "officexapp/types"

// query from database 
const { host, drive_id, org_name } = await readDatabase(MY_ORG_ID)
const { user_id, profile_name, api_key_value } = await readDatabase(`${MY_ORG_ID}_${MY_USER_ID}`)

// send to frontend to inject as cloud auth
const iframe_injected_config: IFrameInjectedConfig = {
  host,
  drive_id,
  org_name,
  user_id,
  profile_name,
  api_key_value,
  redirect_to: `/org/${drive_id}/drive`
}
return iframe_injected_config
```

If your users are often hopping between multiple organizations including entering new ones, we recommend using [deterministic iframe profiles](https://officex.gitbook.io/officex-docs/documentation/core-concepts/authentication#deterministic-iframe-profiles) with cloud organizations, as that lets you avoid a lot of headache managing api keys per user per org. The ephemeral offline profiles can use their crypto identities to generate temp auth signatures as a form of universal auth for all organizations. Compare this with other [common iframe auth flows.](https://officex.gitbook.io/officex-docs/documentation/core-concepts/authentication#common-auth-patterns-for-iframes)



</details>

















