---
author: Elliot Forbes
date: 2017-06-12T15:29:30+01:00
desc: In this article we look at the best practices for designing REST APIs
series: beginner
tags:
  - beginner
  - rest
  - http
title: RESTful API Design - Best Practices
twitter: https://twitter.com/Elliot_F
---

In this article we look at some of the key concepts that everyone should bear in
mind when designing RESTful APIs. These are based off my own experience with
designing and building RESTful APIs in a number of projects and should be taken
with a pinch of salt, I am in no way telling you that you _must_ do it this way.
I am merely

# Versioning

Versioning is incredibly important in pretty much every scenario, be it a
personal project or an enterprise scale service that other teams will be
interfacing with.

When I say versioning your API what I really mean is utilizing a naming
convention for your API endpoints that looks something like so:

```bash
# version: 'v1' of my API
http://myservice.com/api/v1/my-api-endpoint
```

Once you have a stable version of this API deployed, you must not make any
breaking changes to said API. Instead of making large changes, you would instead
add a new API version and expose a new set of endpoints that feature your new
breaking changes and deploy them alongside your existing API:

```bash
# Old untouched API endpoint
http://myservice.com/api/v1/my-api-endpoint
# new breaking API endpoint
http://myservice.com/api/v2/my-api-endpoint
```

By following this approach you are basically guarding yourself from breaking any
other apps that are reliant on your API when you release your new changes. Any
new applications would then use the /v2/ of the API and older apps have plenty
of time to migrate to the new version in their own time.

# Naming Conventions

When it comes to naming your API endpoints you should typically follow a
convention where every endpoint is named the same noun, such as say 'tutorial'
and you would then utilize the various different `HTTP` verbs when it comes to
performing `CRUD` actions against these endpoints.

## Example

Say for instance we have an API that allows us to modify the `users` on our
site. If we wanted a series of endpoints that would allow us to perform CRUD
operations against these users then we should follow this convention:

```bash
POST http://myservice.com/api/v1/user # creates a new user
UPDATE http://myservice.com/api/v1/user # updates a given user
DELETE http://myservice.com/api/v1/user # deletes a given user
GET http://myservice.com/api/v1/user # gets a single user
```



# Discoverability

When it comes to APIs, they should be easily navigable. If you are returning
paginated results then ideally you should include a `next_page` key/value within
your json that directs the user to the next page of results.

# Rate Limiting

We don't typically have unlimited resources when it comes to hosting RESTful
APIs and sometimes we face users of our APIs that abuse them through overuse. If
this happens then rate limiting your APIs can be an effective countermeasure
that stops people from effectively DOSing your services.
