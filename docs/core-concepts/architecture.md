---
description: A Familiar New Paradigm
---

# Architecture

Anonymous OfficeX is a peer-to-peer digital workspace, with privacy, convenience & ownership as core values. Let's explore how the open source software is designed, and the different mental models of understanding below.

### Ephemeral Immortal Apps

OfficeX is designed with the "ephemeral immortal dapp" paradigm. Currently only OfficeX uses this paradigm, but we believe it will become a popular design in software.

From order of simplicity and affordability:

{% stepper %}
{% step %}
### Ephemeral Offline

Clientside apps that work offline with zero dependencies. Free to serve unlimited users. Lowest barrier to entry. Ideal for whitelabel.
{% endstep %}

{% step %}
### Self Hosted / Paid Cloud

Traditional client-server apps with full functionality. Cheap to serve at scale. Can be paid managed cloud, or self hosted. Web2
{% endstep %}

{% step %}
### Immortal DApp

Blockchain-based decentralized apps with sovereign ownership as core principle, while maintaining REST API compatibility as traditional apps. Expensive to serve but users pay for their own gas. Web3
{% endstep %}
{% endstepper %}

All are meant to be as REST API spec compatible as possible. Ephemeral is the advantageous first touchpoint, and users can be graduated to deeper commitment levels. This paradigm is not a silver bullet - but tends to perform well in consumer apps and whitelabel.

<details>

<summary>View Evolutionary Diagram</summary>

Ephemeral Immortal DApps - A new software paradigm

<figure><img src="../.gitbook/assets/ephemeral immortal.jpg" alt=""><figcaption></figcaption></figure>

</details>

### Sovereign vs Custody

OfficeX is designed for both ownership & convenience. In practice, this means the concept of a user is just a permissionless cryptographic identity (aka a crypto wallet, but it is NOT used to hold money). No email, no login with google, every visitor automatically gets a profile in zero clicks.&#x20;

The inherent advantage is that you get a universal identity system across all instances of OfficeX, regardless of how/who/where it runs. All OfficeX users can interact with all OfficeX backend servers because "users" are not defined in any database, rather it emerges from the mathematics of the universe.

What this means in practice is that a user can exist without your database ever knowing, and that person/agent truly owns their user profile (unless they leak their seed phrase/private keys).  Indeed when you look at the concept of a `Contact` in OfficeX, it is merely a user with a name label. `Contact.id` is the same as `User.id`. You can learn more about the offline user creation process in the [Authentication Guide](authentication.md).

Aside from true user ownership of their profiles, it is possible to create those crypto identities on behalf of users. You can see this in action in the [quickstart](https://officex.gitbook.io/officex-docs/documentation/~/changes/41#tab-reuse-existing-ids) where we create users by specifying a `secret_entropy` string, which deterministically creates the same crypto identity each time. App developers can then create api keys per user per organization, and give these revokeable api keys to users. Since the end users only have a revokeable api key, and never know their secret entropy / seed phrase / private keys, they do not own their profiles. We call this "custody" as app developers are responsible for those users. If the end users know their secret entropy / seed phrase / private keys, then they own their accounts and we call this "sovereign".&#x20;

Note that we mention `secret entropy` `seed phrase` `private keys` as if they are the same thing - in this context you can treat them all as the same: "a secret master password that grants true ownership over an account, and if leaked, anyone with it will also be an owner".&#x20;

So now you know the difference between a sovereign vs custody user - do they know their secret master password (sovereign), or just the revokeable api key (custody)?&#x20;

However, workspaces can also be sovereign vs custody (aka free public cloud vs self hosted). When you use OfficeX official cloud, we maintain your workspace backend, fix bugs, and pay cloud costs. When you self host OfficeX yourself, all the responsibility of uptime, patches & billing is liable to you (this is the price of control).&#x20;

Our recommendation? Use our free public cloud but custody your user profiles. This gives you secure convenience & cost savings, while enabling a seamless UX for your users.

<details>

<summary>View Diagram - Control vs Liability Tradeoff</summary>

<figure><img src="../.gitbook/assets/control vs liability tradeoff (1).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>View Diagram - Integration Compass</summary>

Despite what this compass says, you should still use `Free Public Cloud` unless you have strong reasons to self host. The diagram does not account for maintenance costs.

<figure><img src="../.gitbook/assets/integration compass.png" alt=""><figcaption></figcaption></figure>

</details>

### Composability

OfficeX is designed to be composeable with apps and ai agents with zero dependencies. The entire workspace is available, but lightweight enough to be used for a single feature (eg. spreadsheets)

OfficeX is designed to be used in iframes as a whitelabel UX lego in other apps, or a standalone UX destination as part of a larger system.

Since its so easy to [create workspaces & deterministic users](https://officex.gitbook.io/officex-docs/documentation/~/changes/41#tab-reuse-existing-ids), developers can use OfficeX for recurring and throwaway use cases such as:

* Temporary UX for file organization
* Generate spreadsheets, documents, folders
* Private AI chat history
* Throwaway napkin math & drafts
* Organizing research files
* Bulk download destination
* Archiving projects & exports
* Collaborative Sovereign Workspace
* Decentralized Knowledge Base
* Agentic Anytime Workspace
* Hivemind Library

All while having persistence & privacy out-of-box thanks to crypography and our free public cloud.

Due to being 100% open source, peer-to-peer software, OfficeX allows you to:

* Guarantee your entire workspace, privately ran on your own hardware
* Horizontally scaleable to millions simply by abiding by the REST API spec protocol
* Fork the code, change it to meet your needs
* Host your own private intranet work ecosystem
* Run as apocolypse proof workplace OS
* Integrate & automate with blockchains
* Include any storage destination

The possibilities are endless, while the software is standard. No need to reinvent the wheel - clean reliable tools for your AI Agents.

### Storage Agnostic

OfficeX is storage agnostic - it doesn't matter where your end destination is, we have an adapter and anyone can create adapters. Currently we support the following storage destinations:

* ✅ Offline browser cache&#x20;
* ✅ Cloud S3-compatible buckets (amazon, storj)
* ✅ Internet Computer Canisters (dfinity icp)

Coming soon:

* ☑️ IPFS storage (pinata cloud, filecoin)
* ☑️ BLOB storage (walrus, storacha, dfinity)
* ☑️ SSD storage (personal hard drives)
* ☑️ SAAS storage (google drive, microsoft onedrive, dropbox)
* ☑️ MAGNET storage (torrents, peer sync)

By default, all OfficeX installations include offline browser cache storage and 24-hour temporary S3 buckets. Users and app developers can bring their own storage, or rely on our public appstore where storage giftcards can be purchased by 3rd party vendors.

### Multi-Tenant SQLite

OfficeX backend servers are a single docker container with multi-tenant SQLite. Each organization gets its own isolated SQLite database file, which has benefits such as:

* Isolation safety & privacy
* Scale to zero passive persistence
* Minimal system requirements
* Exportable as single encrypted file
* Importable from restore backups
* Runs in both server & browser environments&#x20;

100k organizations can fit inside a single 8gb USB drive.

### Shortlinks

OfficeX includes its own url shortener for filesharing convenience.&#x20;

For portability reasons, OfficeX sometimes serializes complex data into url safe strings so that they can be included in share links without the need for a backend server. These strings can get quite long, so OfficeX provides a default url shortener to help make things easier. This is not paradoxical, it is practical because ephemeral clients can use shared public servers for url shortening. From the pure ephemeral client point of view, they enjoy the benefits of the url shortener without having to self-host.

Every cloud OfficeX instance has its own url shortener capabilties. It is a standard REST API route.

Bonus: Shortlinks can be used to enhance frontend iframe security. Auto-login urls are convenient but dangerous as they hold api keys within the url params. Saving auto-login urls as a shortlink lets developers pass just a shortlink slug to iframes, redirecting users to final auto-login url, without ever exposing api keys directly on frontend transit. The shortlink can be revoked after successful loading.

<details>

<summary>Preview Code Sample</summary>

The below example shows how to use url shortener to hide auto-login urls. This avoids exposing api-keys in transit if you are concerned about that.&#x20;

`create shortlink`

```typescript
import { IRequestShortLink, IResponseShortLink, UserID, DriveID } from "officexapp/types"

const AUTO_LOGIN_URL = "https://officex.app/auto-login?redeem=my-sensitive-login-info-i-want-to-hide"

const payload: IRequestShortLink = {
    // slug?: string;    
    original_url: AUTO_LOGIN_URL
}

const result: IResponseShortLink = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/shortlink`, {
      method: "POST",
      headers: {  
           "Content-Type": "application/json",
           "Authorization": `Bearer ${api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseShortLink {
    slug: string; // use this in the next api call to get original
    original_url: string;
    shortlink_url: string; // use this in browser, it will redirect to original_url
}

console.log(shortlink_url)
// https://officex.app/org/{DriveID}/to/slug
```

`get original`

```typescript
import { IRequestShortLink, IResponseShortLink, UserID, DriveID } from "officexapp/types"

// we can reverse the payload and it will it gives us back the same response 
const payload: IRequestShortLink = {
    slug?: string; // slug will be in the shortlink url, eg "https://officex.app/org/{DriveID}/to/slug" 
    // original_url?: AUTO_LOGIN_URL
}

const result: IResponseShortLink = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/shortlink`, {
      method: "POST",
      headers: {  
           "Content-Type": "application/json",
           "Authorization": `Bearer ${api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

interface IResponseShortLink {
    slug: string;
    original_url: string;
    shortlink_url: string;
}
```

`delete shortlink`

```typescript
import { IRequestShortLink, IResponseShortLink, UserID, DriveID } from "officexapp/types"

// we can delete a shortlink by providing both values
const payload: IRequestShortLink = {
    slug: string;
    original_url: string;
}

const result: IResponseShortLink = await (
    await fetch(`${host}/v1/drive/${DriveID}/organization/shortlink`, {
      method: "POST",
      headers: {  
           "Content-Type": "application/json",
           "Authorization": `Bearer ${api_key}`
      },
      body: JSON.stringify(body),
    })
  ).json();

// returns the old response but now original url goes to 404 not found
interface IResponseShortLink {
    slug: string;
    original_url: string; // https://officex.app/not-found
    shortlink_url: string;
}
```

Purely clientside installations can use public url shortener endpoints, as found in [CONFIG.DEFAULT\_ANON\_SHORTLINK\_HOST](https://github.com/OfficeXApp/Storage/blob/02957fe1bc520ad7863afd4e0b926607a707501e/src/config.ts#L5)

</details>

***

Whether you feel refreshing or confused, the best way to get confident building with OfficeX is by trying it out hands on in our codesandbox/codepen examples, in the [2 min quickstart](../).

