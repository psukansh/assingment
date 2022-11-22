
- [Getting started](#getting-started)

install JSON server:

Created with <3 for front-end developers who need a quick back-end for prototyping and mocking.

* [Egghead.io free video tutorial - Creating demo APIs with json-server](https://egghead.io/lessons/nodejs-creating-demo-apis-with-json-server)
* [JSONPlaceholder - Live running version](https://jsonplaceholder.typicode.com)
* [__My JSON Server__ - no installation required, use your own data](https://my-json-server.typicode.com)

See also:
* :dog: [husky - Git hooks made easy](https://github.com/typicode/husky)
* :owl: [lowdb - local JSON database](https://github.com/typicode/lowdb)
* ✅ [xv - a beautifully simple and capable test runner](https://github.com/typicode/xv)

<p>&nbsp;</p>


<p>&nbsp;</p>

<p align="center">
  <a href="https://tryretool.com/?utm_source=sponsor&utm_campaign=typicode" target="_blank">
    <img src="https://i.imgur.com/IBItATn.png" height="70px">
  </a>
</p>

<p>&nbsp;</p>

<p align="center">
  <a href="https://mockend.com/" target="_blank">
    <img src="https://jsonplaceholder.typicode.com/mockend.svg" height="70px">
  </a>
</p>

<p>&nbsp;</p>

<p align="center">
  <a href="https://megafamous.com/buy-instagram-followers" target="_blank">
    <img src="https://jsonplaceholder.typicode.com/megafamous.png" height="70px">
  </a>
</p>

<p>&nbsp;</p>

<p>&nbsp;</p>

<h2 align="center">Silver sponsors 🥈</h2>

<p>&nbsp;</p>

<p align="center">
  <a href="https://cased.com" target="_blank">
    <img src="https://user-images.githubusercontent.com/5502029/194441951-b7dca49d-efd6-496d-900b-288004717f11.png" height="55px">
  </a>
</p>

<p>&nbsp;</p>

<p>&nbsp;</p>

[Become a sponsor and have your company logo here](https://github.com/users/typicode/sponsorship)

## Sponsor

__Please help me build OSS__ 👉 [GitHub Sponsors](https://github.com/sponsors/typicode) :heart:

## Table of contents

<!-- toc -->

- [Getting started](#getting-started)
- [Routes](#routes)
  * [Plural routes](#plural-routes)
  * [Singular routes](#singular-routes)
  * [Filter](#filter)
  * [Paginate](#paginate)
  * [Sort](#sort)
  * [Slice](#slice)
  * [Operators](#operators)
  * [Full-text search](#full-text-search)
  * [Relationships](#relationships)
  * [Database](#database)
  * [Homepage](#homepage)
- [Extras](#extras)
  * [Static file server](#static-file-server)
  * [Alternative port](#alternative-port)
  * [Access from anywhere](#access-from-anywhere)
  * [Remote schema](#remote-schema)
  * [Generate random data](#generate-random-data)
  * [HTTPS](#https)
  * [Add custom routes](#add-custom-routes)
  * [Add middlewares](#add-middlewares)
  * [CLI usage](#cli-usage)
  * [Module](#module)
    + [Simple example](#simple-example)
    + [Custom routes example](#custom-routes-example)
    + [Access control example](#access-control-example)
    + [Custom output example](#custom-output-example)
    + [Rewriter example](#rewriter-example)
    + [Mounting JSON Server on another endpoint example](#mounting-json-server-on-another-endpoint-example)
    + [API](#api)
  * [Deployment](#deployment)
- [Links](#links)
  * [Video](#video)
  * [Articles](#articles)
  * [Third-party tools](#third-party-tools)
- [License](#license)

<!-- tocstop -->

## Getting started

Install JSON Server 

```
npm install -g json-server
```

Create a `db.json` file with some data

```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

Start JSON Server

```bash
json-server --watch db.json
```

Now if you go to [http://localhost:3000/posts/1](http://localhost:3000/tasks/1), you'll get

```json
{ "id": 1, "title": "json-server", "author": "typicode" }
```

Also when doing requests, it's good to know that:

- If you make POST, PUT, PATCH or DELETE requests, changes will be automatically and safely saved to `db.json` using [lowdb](https://github.com/typicode/lowdb).
- Your request body JSON should be object enclosed, just like the GET output. (for example `{"name": "Foobar"}`)
- Id values are not mutable. Any `id` value in the body of your PUT or PATCH request will be ignored. Only a value set in a POST request will be respected, but only if not already taken.
- A POST, PUT or PATCH request should include a `Content-Type: application/json` header to use the JSON in the request body. Otherwise it will return a 2XX status code, but without changes being made to the data. 

## Routes

Based on the previous `db.json` file, here are all the default routes. You can also add [other routes](#add-custom-routes) using `--routes`.

### Plural routes

```
GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1