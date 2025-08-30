---
description: Welcome to your team’s developer platform
layout:
  width: wide
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: true
---

# Developer Platform

<h2 align="center">OfficeX Developer Platform</h2>

<p align="center">Anonymous Workspaces for Your App</p>

<p align="center"></p>

<p align="center"></p>

{% columns %}
{% column %}
### Get started in 2 minutes

Anonymous OfficeX is designed for whitelabel with zero dependencies.&#x20;

The `/quickstart` endpoint is the easiest way to get started. It will create a new organization, auth credentials & magic login links.

You can reuse your same User IDs and sync anything with your database schema.

Try it in codepen live, or read the "Get Started" guide for full details.

<a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/" class="button primary" data-icon="rocket-launch">Get Started</a> <a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/XdQ7dOsfwiLPSkHYfPSw/" class="button secondary" data-icon="terminal">Run in Codepen</a>
{% endcolumn %}

{% column %}
{% code title="index.js" overflow="wrap" %}
```javascript
// try this in browser js console
const logins = await (
    await fetch(`https://officex.otterpad.cc/v1/factory/quickstart`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        org_name: "Anonymous Org",
        members: [
          { name: "friend1" }, 
          { name: "friend2" }
        ],
      }),
    })
  ).json();
  console.log(logins); 
```
{% endcode %}
{% endcolumn %}
{% endcolumns %}

###

{% columns %}
{% column %}
### iFrame

Anonymous OfficeX can work clientside offline without servers. It's also easy to sync with cloud anytime.

iFrames can be controlled via `iframe.postMessage()` to upload files, navigate routes & more. The REST API can also be used to control remotely.

Try it in codepen live, or read the guide for full details (youtube video available)

<a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/ujkN4BAhyR1QV0VJy9ki/" class="button primary" data-icon="play">Watch Tutorial</a> <a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/" class="button secondary" data-icon="terminal">Run in Codepen</a>
{% endcolumn %}

{% column %}
```html
<iframe
  id="officex-iframe"
  src="https://officex.app"
  sandbox="allow-same-origin allow-scripts allow-downloads allow-popups"
></iframe>
<script>
  const iframeElement = document.getElementById("officex-iframe");
  iframeElement.onload = () => {
    const data = { injected: logins };
    iframeElement.contentWindow.postMessage(
      { type: "OFFICEX_INIT", data, tracer: "my-tracer" },
      "https://officex.app"
    );
  };
</script>
```
{% endcolumn %}
{% endcolumns %}

###

{% columns %}
{% column %}
### REST API

Anonymous OfficeX can work clientside offline without servers. It's also easy to sync with cloud anytime.

iFrames can be controlled via `iframe.postMessage()` to upload files, navigate routes & more

<a href="./" class="button primary" data-icon="book-open">API Reference</a> <a href="./#join-the-developer-community" class="button secondary" data-icon="terminal">Run in Postman</a>




{% endcolumn %}

{% column %}
```
# Simplified for demo, see API reference

POST /directory/action
POST /groups/invite
POST /permits/create
POST /webhooks/create
POST /organization/search
POST /organization/archive
```
{% endcolumn %}
{% endcolumns %}

###

{% columns %}
{% column %}
### Typescript Types

Anonymous OfficeX can work clientside offline without servers. It's also easy to sync with cloud anytime.

<a href="./#officex-developer-platform" class="button primary" data-icon="inbox-in">Npm Package</a> <a href="./#join-the-developer-community" class="button secondary" data-icon="terminal">Run in Codepen</a>
{% endcolumn %}

{% column %}
```typescript
// Simplified for demo, see API reference
import { 
  IRequestCreateContact, 
  IResponseCreateContact 
} from "@officexapp/types";

const payload: IRequestCreateContact = {
  name: string;
  avatar?: string;
  email?: string;
  is_placeholder?: boolean;
}

const result: IResponseCreateContact = await fetch(
  "/contacts/create", 
  { body }
)
```
{% endcolumn %}
{% endcolumns %}

***

<h2 align="center">Anonymous Workspace</h2>

<p align="center">Product Demo | Built for Whitelabel</p>

<figure><img src=".gitbook/assets/demo (1).gif" alt=""><figcaption></figcaption></figure>

***

<h2 align="center">Learn More</h2>

<p align="center">Recommended to start with Core Concepts</p>

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h4><i class="fa-leaf">:leaf:</i></h4></td><td><strong>Core Concepts</strong></td><td>Get started with the developer platform in 5 minutes.</td><td><a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/">Documentation</a></td><td><a href=".gitbook/assets/no-code.jpg">no-code.jpg</a></td></tr><tr><td><h4><i class="fa-terminal">:terminal:</i></h4></td><td><strong>API reference</strong></td><td>Browse, test, and implement APIs.</td><td><a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/XdQ7dOsfwiLPSkHYfPSw/">API Reference</a></td><td><a href=".gitbook/assets/api-reference.jpg">api-reference.jpg</a></td></tr><tr><td><h4><i class="fa-server">:server:</i></h4></td><td><strong>Free Public Cloud</strong></td><td>Learn more about hosting the developer platform.</td><td><a href="https://app.gitbook.com/o/Rx9kiXskWINgQhCguck0/s/JGs1RfAKF1Qf9BDbqCGA/">Documentation</a></td><td><a href=".gitbook/assets/hosted.jpg">hosted.jpg</a></td></tr></tbody></table>

***

<h2 align="center">Join the developer community</h2>

<p align="center">Join our Discord community or create your first PR in just a few steps.</p>

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h4><i class="fa-discord">:discord:</i></h4></td><td><strong>Discord community</strong></td><td>Join our Discord community to post questions, get help, and share resources with like-minded developers.</td><td><a href="https://www.gitbook.com/" class="button secondary">Join Discord</a></td><td></td></tr><tr><td><h4><i class="fa-github">:github:</i></h4></td><td><strong>GitHub</strong></td><td>Our product is 100% open source and built by developers just like you. Head to our GitHub repository to learn how to submit your first PR.</td><td><a href="https://www.gitbook.com/" class="button secondary">Submit a PR</a></td><td></td></tr></tbody></table>
