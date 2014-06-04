---
title: The Unloq API

language_tabs:
  - shell

toc_footers:
  - <a href='http://unloq.co'>Unloq</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

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

Unloq uses API keys to allow access to the API. Your API key should be used with the same care and privacy with which you treat your own systems passwords.

Unloq expects for the API key to be included in all API requests to the server in either the JSON body OR as part of the URI.

# Achievements

Achievements are actionable/unlockable actors which are realized by a single, or stream of Events. They, much like Events, are made up of a set of predicates. If the predicates "match" then the Achievement becomes unlocked.

## Create An Achievement
```shell
curl http://unloq.co/achievements -X POST -H 'Content-Type: application/json' \
--data-binary '{
  "api_key":"YOUR_API_KEY",
  "namespace":"your-namespace",
  "name":"Achievement Name",
  "author_type":"Authoring Type",
  "verb":"Verb",
  "recipient_type":"Recipient Type",
  "recipient_id": "Recipient ID",
  "observations":1,
  "points": 10.0,
  "start_at":null,
  "end_at":null,
  "image_path":"http://my-img-host.com/badge_image.png"
}' -v
```

To create an Achievement, submit a POST request to the /achievements resource as seen in the example to our right:

### JSON Request Attributes

Attribute | Required | Description
:-------------|:-------------:| :-------------
api_key | true | the api key you were provided from unloq. This should be treated as private (just like a password).
namespace | true | the environment in which the event took place.
author_type | true | the type or classification of the acting author.
author_id | false | the id of the acting author performing the action (verb). Used only if a SPECIFIC author should get an achievement.
verb | true | what the author "did" to a recipient
recipient_type| false  | the type or classification of the acting recipient.
recipient_id | false | the id of the actor being acted on (could be the same as the author_id/type). Used only if a SPECIFIC recipient should match the event.





## Get All Namespace Achievements

>Get All Namespace Achievements

```shell
curl "http://unloq.co/achievements/[:api_key]/[:namespace]"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this:

```json
{
    "achievements": [
    {
    "id": "b32c8f3b-d555-4f9b-a4f2-734f6f50bed9",
    "api_key": "[:api_key]",
    "namespace":"[:namespace]",
    "name":"[:name]",
    "author_type":"[:author_type]",
    "verb":"[:verb]",
    "recipient_type":"[:recipient_type]",
    "recipient_id": "[:recipient_id]",
    "start_at": null,
    "image_path":"http://my-img-host.com/badge_image.png",
    "end_at": null,
    "observations": 1,
    "points": 10.0
    }
    ],
"points": null
}

```
`GET http://unloq.co/achievements/[:api_key]/[:namespace]`

Some text about how you use this.

## Get A Users/Authors Achievements

>Get A Users/Authors Achievements

```shell
curl "http://unloq.co/achievements/[:api_key]/[:namespace]/[:author_type]/[:author_id]"
  -H "Content-Type: application/json"
```

> The above command returns JSON structured like this, if, perhaps your Author (User) had 50.0 points
> Notice the difference between querying achievements for the entire namespace returns points: null
> This is because there is no Author in context and therefore, no points associated.

```json
{
    "achievements": [
    {
    "id": "b32c8f3b-d555-4f9b-a4f2-734f6f50bed9",
    "api_key": "[:api_key]",
    "namespace":"[:namespace]",
    "name":"[:name]",
    "author_type":"[:author_type]",
    "verb":"[:verb]",
    "recipient_type":"[:recipient_type]",
    "recipient_id": "[:recipient_id]",
    "start_at": null,
    "image_path":"http://my-img-host.com/badge_image.png",
    "end_at": null,
    "observations": 1,
    "points": 10.0
    }
    ],
"points": 50.0
}
```

`GET http://unloq.co/achievements/[:api_key]/[:namespace]/[:author_type]/[:author_id]`

Some text about how you use this.
