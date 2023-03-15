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

defaults:
  layout: center

layout: intro
---

# API-solutely Fabulous

A crash course on HTTP APIs

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

## Goals

1. To understand what an API is and how to think about them, generally
2. To understand how to talk to an HTTP API
3. To get some hands-on experience doing tasks with an HTTP API

---

## Time Out: Some pre work

1. Sign up for a GitHub account
2. Create a "Classic" Personal Access Token
   - The token should expire in 7 days (we want to make sure it expires quick for reasons I'll get into)
   - The token should have the `repo` and `user` permissions for today
   - The token should be saved someplace safe (i.e. a Password Manager or other secure location)

---
layout: quote
---

You can never understand everything, but you should push yourself to understand the system

-- Ryan Dahl (Creator of Node.js)

---
layout: section
---

## APIs

---

## What is an API

API stands for "Application Programming Interface"

---

### WTF!?

---

## Interface

The way you interact with a thing

---

"Physical User Interface" (PUI)<br />vs<br />"Mechanical Reactive Interface" (MRI)

---

- Sink
  - PUI
    - Inputs: One or more knobs that control the flow of water
    - Outputs: One or more pipes that disperse water
  - MRI
    - Plumbing, filters, sewage, grid, etc

---

- Car
  - PUI
    - Inputs: A wheel, 2-3 foot pedals, & a shifter
    - Outputs: "car go vroom and swerve"
  - MRI
    - The engine, brakes, hydraulics, exhaust, etc.

---

## Interface

How do we learn?

---

### ~~API~~ _HTTP_ API

---

## HTTP

HyperText Transfer Protocol

---

### HTTP: When does it happen?

<br />
<br />

```mermaid
flowchart LR
    user(You)
    client(Browser)
    server(Google)

    user-- Click button ---client
    client--HTTP Request-->server
    server--HTTP Response-->client
```
---

### MOST IMPORTANT

HTTP is "stateless"

---

## HTTP: The Cycle

- Request
  - Comes from a "client" (e.g. your web browser, a CLI, Postman, HTTPie, your SaaS app)
  - Communicates with "verbs", URLs, headers, and payload/body
- Response
  - Comes from a "server" (e.g. A different SaaS app, any device that knows how to respond to HTTP requests)
  - Communicates with response codes, headers, and payload/body

---
layout: full
---

```http{all|1-10|1|5|12-27|all}
HTTP/1.1 200 OK
Age: 0
Cache-Control: public, max-age=0, must-revalidate
Content-Length: 545
Content-Type: text/html; charset=UTF-8
Date: Tue, 14 Mar 2023 19:51:31 GMT
Etag: "a5fdd42b717b530e6175ab91f67037f5-ssl"
Server: Netlify
Strict-Transport-Security: max-age=31536000
X-Nf-Request-Id: 01GVGTV1G1J5K7JE2BGAP4Q91R

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="icon" href="/assets/8b9eb19119592679c97707c257d88026-a02f38e2.png">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@200;400;600&display=swap" type="text/css">
  <script type="module" crossorigin src="/assets/index-cf09b09f.js"></script>
  <link rel="stylesheet" href="/assets/index-9b901fa7.css">
</head>
<body>
  <div id="app"></div>


</body>
</html>
```
---
layout: iframe
url: https://http.cat
---

---
layout: full
---

```http{all|5|1|2|6}
GET / HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Host: apisolutely.birdcar.dev
User-Agent: HTTPie/3.2.1

```

---
layout: full
---

```http{all|1-10|12-15}
POST /repos/birdcar/notes/issues HTTP/1.1
Accept: application/vnd.github+json
Accept-Encoding: gzip, deflate
Authorization: Bearer SECRET_TOKEN_NO_LOOKIE
Connection: keep-alive
Content-Length: 444
Content-Type: application/json
Host: api.github.com
User-Agent: HTTPie/3.2.1
X-GitHub-Api-Version: 2022-11-28

{
  "title": "OMG This is super broken",
  "body": "So like, I know this is a project you build on your free time for your own personal use and have graciously given away for free, and I know that I work for a FAANG company and we could/should have a moral obligation to pay you to maintain this since we built an entire business on it, but honestly that seems hard and it would be great if you worked for free to fix every problem I have. Kthxbye"
}
```

---
layout: section
---

## How server know things if stateless?

---

- HTTP verbs
- URL
- Headers
- Body

---

## Anatomy of HTTP Verbs

- `GET`: I'm looking for something and would like you to give it to me
- `POST`: Here's something I want you to make from scratch
- `PUT/PATCH`: You already know what this is, but please update it for me
- `DELETE`: Lol nuke it from space
- `HEAD`: Just give me the headers for this response

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
            domain_name(github.) --- tld(com)
        end
        subdomains{{api.}} --- DOMAIN
    end
    protocol(https://) --- HOSTNAME --- path(/issues) --- querystring(?filter=created&state=open)
```

---
layout: full
---

## Anatomy of Headers

<br />
<br />

```http{all|1-10|8|1|4|2-3|7}
POST /repos/birdcar/notes/issues HTTP/1.1
Accept: application/vnd.github+json
Accept-Encoding: gzip, deflate
Authorization: Bearer SECRET_TOKEN_NO_LOOKIE
Connection: keep-alive
Content-Length: 444
Content-Type: application/json
Host: api.github.com
User-Agent: HTTPie/3.2.1
X-GitHub-Api-Version: 2022-11-28
```

---
layout: full
---

## Anatomy of (a type of) Body

<br />
<br />

```json
{
  "title": "OMG This is super broken",
  "body": "So like, I know this is a project you build on your free time for your own personal use and have graciously given away for free, and I know that I work for a FAANG company and we could/should have a moral obligation to pay you to maintain this since we built an entire business on it, but honestly that seems hard and it would be great if you worked for free to fix every problem I have. Kthxbye"
}
```

---
layout: section
---

## Go get some REST

---

## REpresentational State Transfer (REST) API

- A type of API that organizes the stuff you can do into "resources"
- Designed to leverage _all_ of the ways HTTP requests can express themselves
- The _dominant_ kind of Web API (You are probably already supporting one in one way or another)

---
layout: full
---

```http
POST /repos/birdcar/notes/issues HTTP/1.1
Accept: application/vnd.github+json
Accept-Encoding: gzip, deflate
Authorization: Bearer SECRET_TOKEN_NO_LOOKIE
Connection: keep-alive
Content-Length: 444
Content-Type: application/json
Host: api.github.com
User-Agent: HTTPie/3.2.1
X-GitHub-Api-Version: 2022-11-28

{
  "title": "OMG This is super broken",
  "body": "So like, I know this is a project you build on your free time for your own personal use and have graciously given away for free, and I know that I work for a FAANG company and we could/should have a moral obligation to pay you to maintain this since we built an entire business on it, but honestly that seems hard and it would be great if you worked for free to fix every problem I have. Kthxbye"
}
```

---
layout: section
---

## Putting it all together: API docs

https://docs.github.com/en/rest/issues/issues

---
layout: section
---
## Q & A

---
layout: section
---

## Hands-on time

---
layout: section
---
## Task 1: Get your GitHub user information

https://docs.github.com/en/rest/users/users?apiVersion=2022-11-28#get-the-authenticated-user

---
layout: section
---

## Task 2: Create an issue in birdcar/apisolutelyfab

https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#create-an-issue

---
layout: section
---

## Task 3: Add a comment to the issue you created

https://docs.github.com/en/rest/issues/comments?apiVersion=2022-11-28#create-an-issue-comment

---
layout: section
---

## Task 4: List all issues created by your user

https://docs.github.com/en/rest/issues/issues?apiVersion=2022-11-28#list-issues-assigned-to-the-authenticated-user
