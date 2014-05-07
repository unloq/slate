---
title: The Unloq API

language_tabs:
  - shell

toc_footers:
  - <a href='http://unloq.co'>Sign Up for an Unloq Account</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Unloq documentation, here you can see which RESTful endpoints
exist, what they do and what they expect and respond to.

We currently only have language bindings in Curl (or "shell") and
would LOVE for you to develop client libaries which we will happily
host here in these very docs for all to see.

In the documentation below, we'll cover the key pieces (Events and
Achievements) of our system and provide you with real world examples
in each section.

Remember, if you have any questions about modeling events, don't
hesitate to reach out to us via email - it's always on...always!

This example API documentation page was created with [Slate](http://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Overview

Unloq is based on a concept of receiving Events in order to "unlock"
or achieve - which ever you prefer, Achievements for points in a form
of competition between authors.

Authors are generally just your users and generally have an identifier
to determine which user is which in a given system. Similarly, these
authors perform actions on objects in systems (yours, in fact) and we
refer to those objects as Recipients. For example, if your system were
a blog, you may have a User and that User may have Posts. Both the
User and a Post have that identification which makes them unique in
your system (generally your primary key). When a User creates a Post
this is a relatable event within your system that has a lot of
meaning.

In Unloq, you simply define the parameters of what occurred in that
event so that you might gain insight through intentional context
(think meta information) when Users (or any object in your system for
that matter) perform actions (we call them Verbs) on other objects
(Recipients). And of course, there is nothing which says an Author
can't act upon itself. Some clients prefer to count a User logging in
as an action on themselves. The parameters of this Event would be that
the author "User 14" "login" "User 14" - or more readably to a human:
User 14 logged in.

The simplicity of our system is often one which is misunderstood at
first, but once the modeling of events becomes familiar, you'll
quickly see all sorts of context that's going on in your applications
and systems which can provide all sorts of great insight.


# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve
