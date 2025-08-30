---
description: OfficeX Cryptographic Guarantees
---

# Authentication

User Authentication on OfficeX uses either `plain string api keys`, or `cryptographic identities`, to represent a user. Crypto auth is powerful because it enables native integration between blockchain systems, offline systems & sovereign ownership of accounts.

What are the implications?

* Organizations can have a multi-sig as owner superadmin
* AI Agents can own their own sovereign profiles
* Systems can work together without a single centralized auth authority
* Seamless composability/compatibility between offline, web2 & web3
* Workspaces can be fully encrypted and archived without active computers managing it

Recall that every user in OfficeX is really just a crypto wallet. The user id is just a public key (specifically [ICP principal ](https://internetcomputer.org/docs/tutorials/developer-liftoff/level-3/3.5-identities-and-auth)on Internet Computer Protocol blockchain). This is what a typical OfficeX user id looks like.&#x20;

```
UserID_b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae
```

The prefix `UserID_` just denotes its an OfficeX user. The suffix `b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae` is the actual public key address of the crypto wallet (ICP principal).

### Auth Flows Compared

While very powerful, crypo-native authentication is a minimum resort. The easiest and recommended way to manage auth in OfficeX is to use plain string api keys. These are the two auth patterns in OfficeX:

1. ✅ Plain string api key
2. ✅ Temporary Crypto Auth Signatures

Lets compare the two:

<table><thead><tr><th width="183.83984375">Attribute</th><th>Plain String API Key</th><th>Temp Crypto Auth Signatures</th></tr></thead><tbody><tr><td>What is it?</td><td>A plain string api key with option of start &#x26; expiry date. </td><td>Crypto wallet signs a temporary signature to act as an ephemeral api key.</td></tr><tr><td>When to use it?</td><td><ul><li>90% of use cases, choose this by default.</li><li>When you want to manage multiple logins for same user.</li><li>Delegated logins that can be revoked</li></ul></td><td><ul><li>When you want a user to be a multi-sig.</li><li>When you have unlimited users and can't give them all an API key in each workspace.</li></ul></td></tr><tr><td>Why use it? (pros)</td><td><ul><li>Simple and practical</li><li>Easy to issue, revoke &#x26; cycle keys</li><li>Can safely manage multiple</li></ul></td><td><ul><li>Sovereign ownership guarantees. </li><li>Passively works, dont need to manage any api keys.</li><li>Works as a "universal api key" for any organization</li></ul></td></tr><tr><td>Risks (cons)</td><td><ul><li>Requires active management. 100 orgs x 100 users = 10,000 api keys </li><li>Must be a contact in an org in order for user to have an API key</li></ul></td><td><ul><li>Private keys are unrevokeable. If exposed, its permanently leaked.</li></ul></td></tr></tbody></table>

Both options are compatible with AI Agents and human users. When in doubt, use `plain string api key`&#x20;



OfficeX does NOT support any of the below auth flows:

1. ❌  JSON web tokens
2. ❌  OAuth 2.0 / OIDC
3. ❌  SAML
4. ❌  Username Password
5. ❌  Email / Sign in with Google Apple Socials
6. ❌  2FA / Multi factor authentication&#x20;

While we do not support these other auth flows, anyone can permissionlessly build workarounds. For example it would be relatively trivial to build an email wrapper around plain string api keys.&#x20;

### How to create OfficeX Users

If you recall from the [Advanced Setup Guide](https://officex.gitbook.io/officex-docs/documentation/getting-started/advanced-setup#create-your-admin-identity), there are 3+1 ways to create an OfficeX user:

1. Self Custody External ICP wallet (Internet Computer wallet such as [Plug Wallet](https://plugwallet.ooo/), [OISY Wallet](https://oisy.com/))
2. Convenience cloud route `/generate-crypto-identity`
3. Offline using your own code (most securely scaleable)
4. Manually on web app [https://officex.app](https://officex.app/)&#x20;

We recommend using Option #2 of `/generate-crypto-identity` as its the easiest and flexibly adapts to your database user ids. Understand the tradeoffs below.

<details>

<summary>Option #1 - Self Custody External ICP Wallet</summary>

Choose this option if you want to use a multi-sig as the superadmin owner of the workspace. This is particularly useful if you are a DAO (decentralized autonomous organization).

```
1. Download your ICP wallet and copy the principal id of your wallet
2. Append `UserID_` to it, and its now a valid OfficeX UserID

For example:
const principal_id = "b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae";
const officex_user_id = `UserID_${principal_id}`

console.log(officex_user_id)
// returns "UserID_b5sy2-4ramt-jojso-cqmlj-rxwek-xe3f6-6tuez-zhrl2-pi65a-dtcd6-tae"
```

</details>

<details>

<summary>Option #2 - Convenience cloud route /generate-crypto-identity</summary>

Choose this option if you want convenience. Our free public cloud will handle creating the user. Beware of unofficial servers that may log your generated crypto identities. While those crypto wallets are not used to hold money, they can sign 30 second auth tokens to interact with REST API on your behalf.

Only trust servers from the domain `officex.app` or `anonwork.space` , for example, `https://us-east-1.officex.app` or `https://ap-northeast-1.anonwork.space` . We maintain a list of valid domains further down in this page.

The `secret_entropy` can be any string, often a concatenation of your database user id plus some secret string. It will lead to the same deterministic user generated every time.

The `seed_phrase` , if you choose to use this method, must be a valid BIP-39 Mnemonic Seed from [this wordlist.](https://www.blockplate.com/pages/bip-39-wordlist) Both methods are valid, we recommend using `secret_entropy` as its flexibly adaptable to your existing user ids.

```typescript
import { IRequestGenerateCryptoIdentity } from "officexapp/types"

const payload: IRequestGenerateCryptoIdentity = {
    secret_entropy?: string; // this can be any string
    seed_phrase?: string; // if using this, make sure its a valid "BIP-39 Mnemonic Seed"
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

</details>

<details>

<summary>Option #3 - Offline using your own code</summary>

Choose this option if you want to maintain a high bar of security over custodial users while using 3rd party servers. It is simply running the same code that powers Option #2 `/generate-crypto-identity` , except on your own offline servers.

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

<summary>Option #4 - Manually on Web App </summary>

Easily create a new OfficeX user in your web browser. Simply navigate to [https://officex.app](https://officex.app/) and at the top right, click the users dropdown and create new profile.

<figure><img src="../.gitbook/assets/Untitledfdsa.gif" alt=""><figcaption></figcaption></figure>

</details>

Once you've created an OfficeX user, you can decide which authentication flow to give them. Continue reading to learn more.



### Temporary Crypto Auth Signatures

Recall that every user in OfficeX is really just a crypto wallet. The user id is just a public key (specifically [ICP principal ](https://internetcomputer.org/docs/tutorials/developer-liftoff/level-3/3.5-identities-and-auth)on Internet Computer Protocol blockchain). This implies the existence of a private key which can be used to sign cryptographic signatures. Indeed this possible.

On the webapp frontend, if your profile was created by you on the webapp, it should have private keys in the web browser browser storage. You can check by navigating to the Settings page and in the profile section, click the `Generate Signature` button to get a temp auth signature. See GIF below:

<figure><img src="../.gitbook/assets/sign.gif" alt=""><figcaption></figcaption></figure>

If you are unable to generate a temporary auth signature, it means you do not have private key in your browser storage and thus cannot use this auth flow. This will be the reality for most custodied users who login with API keys or auto-login urls.&#x20;

This same process can be done offline in your own backend. Here is what that looks like:

<details>

<summary>Offline Generate Temp Auth Signature </summary>

Generating a signature can be done by anyone as long as they have the private key or seed phrase to create an ICP principal identity. The `@dfinity/identity` npm package handles signing for us, as seen in the code below, which returns the final temp auth signature string.

Pro-Tip: You can create temp auth signatures for a 30 second period in the future by changing the `challenge.timestamp_ms` value. By default, all OfficeX servers only accept a temp auth signature if the timestamp was in the last 30 seconds. If you are self hosting, you can change this [acceptable time window here.](https://github.com/OfficeXApp/typescript-server/blob/79c032cc721b31125d0272d6385b725296565b40/src/services/auth.ts#L183-L188)

<a href="https://codesandbox.io/p/sandbox/generate-crypto-identities-officex-sn95h3" class="button primary" data-icon="terminal">Run in Codepen</a>

```typescript
import { mnemonicToSeedSync } from "@scure/bip39";
import { Ed25519KeyIdentity } from "@dfinity/identity";
import { DriveID } from "@officexapp/types";

/**
 * Derives a 32-byte Ed25519 key from a seed using SHA-256.
 *
 * @param seed The Uint8Array seed to derive the key from.
 * @returns A Promise that resolves to the 32-byte derived key.
 */
const deriveEd25519KeyFromSeed = async (
  seed: Uint8Array
): Promise<Uint8Array> => {
  const hashBuffer = await crypto.subtle.digest("SHA-256", seed);
  return new Uint8Array(hashBuffer).slice(0, 32);
};

/**
 * Generates an ICP authentication signature.
 *
 * @param seedPhrase The BIP-39 mnemonic phrase to derive the ICP identity.
 * @param driveId The drive's canister ID (represented as an ICP public address).
 * @returns A Promise that resolves to a Base64 encoded signature token string.
 */
export const generateSignature = async (
  seedPhrase: string,
  driveId: DriveID
): Promise<string> => {
  if (!seedPhrase || !driveId) {
    throw new Error("Seed phrase and drive ID are required.");
  }

  try {
    const derivedKey = await deriveEd25519KeyFromSeed(
      mnemonicToSeedSync(seedPhrase)
    );
    const identity = Ed25519KeyIdentity.fromSecretKey(derivedKey);

    const rawPublicKey = identity.getPublicKey().toRaw();
    const publicKeyArray = Array.from(new Uint8Array(rawPublicKey));
    const canonicalPrincipal = identity.getPrincipal().toString();
    const now = Date.now();

    const challenge = {
      timestamp_ms: now, // this can be changed to future date as well
      drive_canister_id: driveId,
      self_auth_principal: publicKeyArray,
      canonical_principal: canonicalPrincipal,
    };

    const challengeBytes = new TextEncoder().encode(JSON.stringify(challenge));

    const signature = await identity.sign(challengeBytes);
    const signatureArray = Array.from(new Uint8Array(signature));

    const proof = {
      auth_type: "SIGNATURE",
      challenge,
      signature: signatureArray,
    };

    const sig_token = btoa(JSON.stringify(proof));

    return sig_token;
  } catch (error) {
    console.error("Signature generation error:", error);
    return "";
  }
};

```

</details>

You can test if the temp auth signature is valid by using it in a REST API call, replacing the header `Authorization: Bearer your_temp_auth_signature` like the code below. It should return the `/whoami` response validly.

```typescript
import { IResponseWhoAmI, DriveID } from "officexapp/types"

const YOUR_TEMP_AUTH_SIGNATURE = "__________________"

const admin: IResponseWhoAmI = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/whoami`, {
      method: "GET",
      headers: { 
          "Content-Type": "application/json",
          "Authorization": `Bearer ${YOUR_TEMP_AUTH_SIGNATURE}`
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

Remember that temp auth signatures are a minimum authentication method, yet also have the higher requirement that the user truely owns the profile by knowing the crypto private keys/seed phrase. It is unique in this way, but for most cases you'll want to give your users plain string api keys.

### Plain String API Keys

Plain string api keys are the recommended default way to give your users access to OfficeX. It is simple, practical & safer thanks to revokeability. The only downside is that you need to create a contact to represent each user in an organization, which implies you are using code to automate this process. That code looks like this:

1. Create a contact inside the organization
2. Create an api key for that contact, inside the organization

To simplify the process, you should use the owner superadmin api keys (or any user with permit to create contacts and api keys for users).&#x20;

Here is what the code looks like to create contact & api key for a user:

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

You can also sanity check the validity of the new api key by calling the `/whoami` endpoint.

Pro-Tips:

1. Take advantage of the `IRequestCreateApiKey.begins_at` and `IRequestCreateApiKey.expires_at` values to time scope the validity of your api keys. For example, only granting access for 24 hours.
2. You can make multiple api keys for a user. This is useful for delegating auth to 3rd party apps and AI Agents. It is highly recommended that every 3rd party app get its own api key so that its easy to revoke access later if need.



### Deterministic iFrame Profiles

If you are using an [ephemeral offline iframe](https://officex.gitbook.io/officex-docs/documentation/getting-started/iframe-guide#tab-ephemeral-offline-mode), then users enjoy temp auth signatures as a form of universal auth for interacting with any officex organization.&#x20;

Simply use the exact same `profile_entropy` string to deterministically give your users the exact same user id on iframe frontends. Below code shows how the child iframe handles auth - the profile now holds a crypto wallet with private key & seed phrase on the client browser frontend, which means it can generate temp auth signatures.&#x20;

Compare this with api keys which need to be generated per user per organization, which is a lot of extra maintenance. Especially if you also need to handle frontend cache clearing. It is just much simpler to use deterministic iframe profiles.

```html
<script>
  const config = {
    profile_name: 'Anon'
    profile_entropy: `${your_user_id}_${any_secret_string}`, // this generates deterministic UserID
    org_name: 'YouTube Downloader App',
    org_entropy: `my_browser_session_id`,
  }
  const iframeElement = document.getElementById("officex-iframe");
  iframeElement.onload = () => {
    iframeElement.contentWindow.postMessage(
      { type: "officex-init", data: { ephemeral: config }, tracer: "my-tracer" },
      "https://officex.app"
    );
  };
</script>
```

While you can choose what `profile_entropy` string to pass in via iframe, the actual final `secret_entropy` will be a concatenation with your domain hostname. You can see the [exact code on Github.](https://github.com/OfficeXApp/Storage/blob/13ab6afefa6ea3e5d182d943d3212154c6e309de/src/framework/iframe/index.tsx#L335-L337)

```typescript
const profile_entropy = `${your_user_id}_${secret_per_user}`
const DOMAIN = "your-website.com"
const final_secret_entropy = `${DOMAIN}-profile-${profile_entropy}`
```

The expected crypto identity generated from this `final_secret_entropy` will be the same as if you called the helper function `/generate-crypto-identity` like so:

```typescript
import { IRequestGenerateCryptoIdentity } from "officexapp/types"

const payload: IRequestGenerateCryptoIdentity = {
    secret_entropy: final_secret_entropy // pass in the final string here
};

const admin: IResponseGenerateCryptoIdentity = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/helpers/generate-crypto-identity`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseGenerateCryptoIdentity {
  user_id: UserID; // this will match the user_id generated by child iframe
  icp_principal: string;
  evm_public_key: string;
  evm_private_key: string;
  origin: {
    secret_entropy?: string;
    seed_phrase?: string;
  };
}
```

The significance of this is that you can predict what officex user ids will be, and they can all generate temp auth signatures for universal auth (webapp auto-handles using temp auth signatures for REST API calls, in the absence of api key).&#x20;

Now the user can interact with any workspace without needing to create contacts or api keys. This can simplify frontend user management significantly. To be percise, it would look like this:

* Your frontend renders an ephemeral iframe with known `profile_entropy` , allowing you to  anticipate what their officex user id would be
* You can let users hop between multiple officex organizations simply by using [iframe navigation.](https://officex.gitbook.io/officex-docs/documentation/~/changes/37/getting-started/iframe-guide#iframecommandtype.navigate) When the iframe changes to the other org, your users might not even have api keys for that org, which is totally okay because ephemeral mode can sign temp auth signatures, as a form of universal authentication.&#x20;
* Even if browser cache is wiped, its easy to load the profile again simply by passing in the exact same `profile_entropy` string

This is what the iframe navigation looks like. When the organization changes, the iframe webapp will automatically handle generating the right temp auth signature for whichever org we are in.

```typescript
import { IFrameCommandType, IFrameCommandReq_Navigate, DriveID } from "officexapp/types"

const message: IFrameCommand = {
  type: IFrameCommandType.NAVIGATE,
  data: { route: `/org/${DriveID}/settings` } as IFrameCommandReq_Navigate,
  tracer: "my-tracer",
};
iframeRef.current.contentWindow.postMessage(message, iframeOrigin);
```

The alternative is that you create an api key per user per organization, and inject those cloud credentials into your iframe once for each org. But if browser cache is wiped, you'll need to inject those credentials again. So ephemeral offline actually works very with cloud based organizations.

Pro-Tips:

1. To improve frontend security for your users, avoid using a universal secret in your `profile_entropy`. Instead you can give each user their own secret. The risk of universal secret is that if it gets leaked, then hackers can predict the officex crypto identities of any of your users. However you may need to also track the custom secret per user in your own database, for convenient reference.



### Common Auth Patterns for iFrames

Sometimes it is not obvious what is the best way to grant your users authenticated access via iframe. To make it easier, we've categorized the scenerios into the below table. If you are not sure which to use, go with `Deterministic iFrame Profiles`

<table><thead><tr><th width="167.3203125">Pattern</th><th>What is it?</th><th>Use Case</th><th>Tradeoffs</th></tr></thead><tbody><tr><td>Deterministic iFrame Profiles</td><td>Your each user has a single user id that is logged in via <code>profile_entropy</code> within iframe. Can create temp auth signatures to use as universal auth.</td><td><ul><li>Recommended for most apps</li><li>Keeping things simple</li></ul></td><td><ul><li>Simplicity</li><li>Unlimited organizations</li><li>Risk of permanently leaking private key</li></ul></td></tr><tr><td>Single Injected Cloud API Key</td><td>Your each user has a single user id that is logged in via injected cloud auth. Users have api key but cannot create temp auth signatures.</td><td><ul><li>When you expect users to only interact with a single organization.</li></ul></td><td><ul><li>Simplicity</li><li>Safely revokeable </li><li>Limited to 1 organization</li></ul></td></tr><tr><td>Multi Injected Cloud API Keys</td><td>Your users can have multiple officex user accounts, or api keys for multiple organizations. Users have api keys but cannot create temp auth signatures.</td><td><ul><li>When you need fine granular control over security and user experience</li></ul></td><td><ul><li>Most granular security</li><li>Safely revokeable </li><li>Most complex moving parts (particularly on frontend cache)</li></ul></td></tr></tbody></table>



### Auto-Login URLs

The concept of an auto-login url is simply a special frontend route that expects an api key encoded within url params. When visited, it handles the entire process of logging in the user, saving them effort and providing a seamless experience.

There are two ways to get an auto-login url:

1. Manually via web app `settings > contacts` page
2. Programmatically via REST API

<details>

<summary>Method #1 - Manually via Web App</summary>

You can generate an auto-login url via web app at the `settings > contacts` pages. See the below GIF as guide.

<figure><img src="../.gitbook/assets/auto-login link.gif" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Method #2 - Programmatically via REST API</summary>

You can get auto-login urls from several possible REST API routes:

* `/quickstart`&#x20;
* `/generate-auto-login-link`

View the [quickstart guide](https://officex.gitbook.io/officex-docs/documentation) to see how it returns auto-login urls.&#x20;

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



### Restore Profile from Seed Phrase

Since OfficeX users are crypto wallets, it is possible to import users via seed phrase. There are two ways to do this:

1. Manually via web app `new profile > import from seed`
2. Programmatically via REST API&#x20;

<details>

<summary>Method #1 - Manually via Web App</summary>

Visit [https://officex.app](https://officex.app/) and click the profile dropdown at top right, click `add profile > import from seed`&#x20;

<figure><img src="../.gitbook/assets/restore from seed.gif" alt=""><figcaption></figcaption></figure>



</details>

<details>

<summary>Method #2 - Programmatically via REST API</summary>

The [typical workflows](https://officex.gitbook.io/officex-docs/documentation/getting-started/advanced-setup#create-your-admin-identity) for creating a crypto identity can be used to restore profiles from seed phrase. The easiest way is to use the REST API route `/generate-crypto-identity`

You can also do it offline in your own private server code. See the typical workflows link above for reference.

<a href="https://codesandbox.io/p/sandbox/generate-crypto-identities-officex-sn95h3" class="button primary" data-icon="terminal">Run in Codepen</a>

</details>



### Bypass iFrame Auth using Shortlinks <a href="#bypass-iframe-auth-using-shortlinks" id="bypass-iframe-auth-using-shortlinks"></a>

The below special route lets you create shortlinks. You can use it to turn auto-login urls into a short slug to be passed into iframes (thus avoid sending auth credentials to frontends). After user successfully redirects and auto-login, you can revoke the shortlink. See how it works [on Github.](https://github.com/OfficeXApp/typescript-server/blob/79c032cc721b31125d0272d6385b725296565b40/src/routes/v1/drive/organization/handlers.ts#L1170)

<details>

<summary>Bypass iFrame Auth using Shortlinks</summary>



</details>



Whenever you are unsure about something, its easy to try it out in production [https://officex.app](https://officex.app/) or in the various codepen examples. The best way to get confident building with OfficeX is by trying it out hands on in our codesandbox/codepen examples, in the [2 min quickstart](../).

