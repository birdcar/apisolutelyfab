---
# Learn more: https://sli.dev/themes/use.html
theme: 'default'
# title of your slide, will auto infer from the first header if not specified
title: "API-solutely Fabulous"
# titleTemplate for the webpage, `%s` will be replaced by the page's title
titleTemplate: '%s - Yetto'
# information for your slides, can be a markdown string
info: false

# enable presenter mode, can be boolean, 'dev' or 'build'
presenter: false

# syntax highlighter, can be 'prism' or 'shiki'
highlighter: 'shiki'
# show line numbers in code blocks
lineNumbers: true
# enable monaco editor, can be boolean, 'dev' or 'build'
monaco: false
# download remote assets in local using vite-plugin-remote-assets, can be boolean, 'dev' or 'build'
remoteAssets: true
# controls whether texts in slides are selectable
selectable: true
# enable slide recording, can be boolean, 'dev' or 'build'
record: 'dev'

# force color schema for the slides, can be 'auto', 'light', or 'dark'
colorSchema: 'dark'
# router mode for vue-router, can be "history" or "hash"
routerMode: 'history'
# aspect ratio for the slides
aspectRatio: '16/9'
# real width of the canvas, unit in px
canvasWidth: 980
# used for theme customization, will inject root styles as `--slidev-theme-x` for attribute `x`
themeConfig:
  primary: '#a21caf'

# favicon, can be a local file path or URL
favicon: 'https://cdn.jsdelivr.net/gh/slidevjs/slidev/assets/favicon.png'
# URL of PlantUML server used to render diagrams
plantUmlServer: 'https://www.plantuml.com/plantuml'
# fonts will be auto imported from Google fonts
# Learn more: https://sli.dev/custom/fonts
fonts:
  sans: 'Fira Code'
  serif: 'Fira Code'
  mono: 'Fira Code'

drawings:
  enabled: true
  persist: false
  presenterOnly: false
  syncAll: true

layout: intro
---

# API-solutely Fabulous

A crash course on HTTP APIs

---
layout: center
---

<img src="https://github.com/birdcar.png" class="mx-auto w-40 rounded-full shadow" />

**Nick Cannariato** (aka. **@birdcar**)

Co-founder / Product @ Yetto


---
layout: default
---

## Places I've supported

<div class="py-24 sm:py-24">
  <div class="mx-auto max-w-7xl px-6 lg:px-8">
    <div class="-mx-6 grid grid-cols-2 gap-0.5 overflow-hidden sm:mx-0 sm:rounded-2xl md:grid-cols-3">
      <div class="bg-zinc-600/5 p-8 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/github.png" alt="GitHub" width="158" height="48">
      </div>
      <div class="bg-zinc-600/5 p-6 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/twilio.png" alt="Twilio" width="158" height="48">
      </div>
      <div class="bg-zinc-600/5 p-6 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/zapier.png" alt="Zapier" width="158" height="48">
      </div>
      <div class="bg-zinc-600/5 p-6 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/heroku.png" alt="Heroku" width="158" height="48">
      </div>
      <div class="bg-zinc-600/5 p-6 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/goabstract.png" alt="Abstract" width="158" height="48">
      </div>
      <div class="bg-zinc-600/5 p-6 sm:p-10">
        <img class="max-h-12 w-full object-contain" src="https://github.com/coin-tracker.png" alt="CoinTracker" width="158" height="48">
      </div>
    </div>
  </div>
</div>

<style>
  h2 {
    text-align: center;
  }
</style>

---
layout: quote
---

You can never understand everything, but you should push yourself to understand the system

-- Ryan Dahl (Creator of Node.js)

---
layout: section
---

## What is an API?

---
layout: center
---

## What is an API

API stands for "Application Programming Interface"

...but wtf does any of that mean?

---
layout: center
---

How *you* think you're opening a Google Doc

<br />
<br />

```mermaid
sequenceDiagram
    You->>Google: Can I haz this Google Doc?
    Google->>You: Yep! Here you go
```

---
layout: center
---

The (very simplified) reality of what's happening in the background

<br />
<br />

```mermaid
sequenceDiagram
    You->>Browser: Ask Google "Can I haz this Google Doc?"
    Browser->>You: Sure, gimme a sec (Loading)
    Browser->>Google: 1. Check if Google is awake and listening
    Browser-->>Google: Hello! Are you awake? Can you hear me?
    Google-->>Browser: Yes! I am awake and can hear you, can you hear me?
    Browser-->>Google: Great!
    Browser->>Google: 2. Request the doc, now that they're listening
    Browser-->>Google: I'm looking for this google doc, can you give that to me?
    Google->>Browser: Yep! Looks like you're allowed to see that, here you go!
    Browser->>You: Here's the doc! (Render page)
```

---
layout: full
---

## Headers

```http{all|1|5|all}
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Mon, 18 Jul 2016 16:06:00 GMT
Etag: "c561c68d0ba92bbeb8b0f612a9199f722e3a621a"
Keep-Alive: timeout=5, max=997
Last-Modified: Mon, 18 Jul 2016 02:36:04 GMT
Server: Apache
Set-Cookie: mykey=myvalue; expires=Mon, 17-Jul-2017 16:06:00 GMT; Max-Age=31449600; Path=/; secure
Transfer-Encoding: chunked
Vary: Cookie, Accept-Encoding
X-Backend-Server: developer2.webapp.scl3.mozilla.com
X-Cache-Info: not cacheable; meta data too large
X-kuma-revision: 1085259
x-frame-options: DENY

{...}
```

---
layout: full
---

## Anatomy of a URL

<br />
<br />
<br />
<br />

```mermaid
flowchart LR
    subgraph HOSTNAME
        direction LR
        subgraph DOMAIN
            direction LR
            domain_name --- tld
        end
        subdomains --- DOMAIN
    end
    protocol---HOSTNAME---path---querystring
```

---
layout: full
---

## Anatomy of a URL

<br />
<br />
<br />
<br />

```mermaid
flowchart LR
    subgraph HOSTNAME
        direction LR
        subgraph DOMAIN
            direction LR
            domain_name{{github.}} --- tld{{com}}
        end
        subdomains{{api.}} --- DOMAIN
    end
    protocol{{https://}} --- HOSTNAME --- path{{/user}} --- querystring{{?label=plugs&label=feature_request}}
```
