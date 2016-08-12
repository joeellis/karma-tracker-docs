---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://github.com/joeellis/karma-tracker'>Github Repo</a>

includes:
  - errors

search: true
---

# Introduction

## What is Karma and why would I want to track it?

Sometimes at your workplace or organization, you want to show your appreciation to your coworker or teammate, perhaps for some outstanding work they've done, or for a funny comment they made.  

You can do this by giving them some __karma__ (sometimes called "kudos", "good feeling", "snaps", or "thanks"), which we keep track in terms of a simple point system.  Then, your coworker can feel rad because they got a little reward, and you can feel rad for making your coworker rad.  So, in the end, everyone gets to be rad.

This Karma Tracker API is a simple RESTful-interface for creating, giving, and tracking karma.  This API works best in tandem with chatbots or automated hooks for Slack, HipChat, Github, etc. so karma can easily be created within your company's everyday chat software and workflow.

## Install

Read the instructions on how to install your own Karma Tracker application on the [github repo](https://github.com/joeellis/karma-tracker) - it should get you setup in running the development server as well as the docs server.

## Coming soon!

- User authentication and authorization
- Slack app integration
- Ability to write custom extensions to provide custom logic for calculating and sending karma

# Users

## The user object

```json
{
  "data": {
    "id": 1,
    "email": "joe@example.com",
    "name": "Joe Ellis",
    "updated_at": 1466737045,
    "inserted_at": 1466737045
  }
}
```

The user object is an object with a data property that contains the following properties of a given user record:

Attribute | Description
--------- | ------- | -----------
id  | ID of the user record.
email | Email of the user.
name | Full name of user.
updated_at | Unix timestamp when record was last updated.
inserted_at | Unix timestamp when record was created.





## List all users

> Example request:

```shell
curl "http://example.com/v1/users"
```

> Returned JSON:

```json
{
  "data": [
    {
      "id": 1,
      "email": "joe@example.com",
      "name": "Joe Ellis",
      "updated_at": 1466737045,
      "inserted_at": 1466737045
    }
  ]
}
```

Returns a list of all users on the system.

### HTTP Request

`GET http://example.com/v1/users`

### Returns

An object with a data property that contains an array of all user objects in the system, ordered by ID. Each entry in the array is a separate user object.





## Retrieve a user

> Example request:

```shell
curl "http://example.com/v1/users/1"
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "email": "joe@example.com",
    "name": "Joe Ellis",
    "updated_at": 1466737045,
    "inserted_at": 1466737045
  }
}
```

Returns a specific user.

### HTTP Request

`GET http://example.com/v1/users/<user_id>`

### Returns

Returns a user object if a valid identifier was provided.





## Create a user

> Example request:

```shell
curl -v -X POST http://example.com/v1/users \
     -H "Content-Type:application/json" \
     -d '{
           "user": {
             "email": "foo@example.com",
             "name": "Foo Bar"
           }
         }'
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "email": "foo@example.com",
    "name": "Foo Bar",
    "updated_at": 1466737045,
    "inserted_at": 1466737045
  }
}
```

Creates a new user object.

### HTTP Request

`POST http://example.com/v1/users`

### Returns

Returns the created user object if the call succeeded.

### Arguments

User parameters must be all wrapped in a `user` namespace before submitting.  Acceptable parameters are as follows:

Parameter | Description
--------- | -----------
email (required) | Email of the user.
name (required) | Full name of the user.





## Update a user

> Example request:

```shell
curl -v -X PUT http://example.com/v1/users/1 \
     -H "Content-Type:application/json" \
     -d '{
           "user": {
             "email": "bar@example.com",
             "name": "Bar Foo"
           }
         }'
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "email": "bar@example.com",
    "name": "Bar Foo",
    "updated_at": 1466737045,
    "inserted_at": 1466737045
  }
}
```

Updates an existing user object.

### HTTP Request

`PUT http://example.com/v1/users/<user_id>`

### Returns

Returns the updated user object if the call succeeded.

### Arguments

User parameters must be all wrapped in a `user` namespace before submitting.  Acceptable parameters are as follows:

Parameter | Description
--------- | -----------
email | New email of the user.
name | New full name of the user.





## Delete a user

> Example request:

```shell
curl -v -X DELETE http://example.com/v1/users/1 \
     -H "Content-Type:application/json"
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "email": "bar@example.com",
    "name": "Bar Foo",
    "updated_at": 1466737045,
    "inserted_at": 1466737045
  }
}
```

Deletes an existing user object.

### HTTP Request

`DELETE http://example.com/v1/users/<user_id>`

### Returns

Returns the deleted user object if the call succeeded.





# Karma

## The karma object

```json
{
  "data": {
    "id": 1,
    "reason": "Helped me figure out some code!",
    "type": "points",
    "amount": 1,
    "giver_id": 1,
    "receiver_id": 2,
    "inserted_at": 1466737045,
    "updated_at": 1466737045
  }
}
```

The karma object is an object with a data property that contains the following properties of a given karma record:

Attribute | Description
--------- | ------- | -----------
id  | ID of the karma record.
giver_id | ID of the user that gave the karma.
receiver_id | ID of the user that received the karma.
reason | Reason / explanation of why the karma was given.
type | The type of karma (can be anything, e.g. points, unicorns, etc). Defaults to "points".
amount | The number of karma given.
updated_at | Unix timestamp when record was last updated.
inserted_at | Unix timestamp when record was created.




## List all karma

> Example request:

```shell
curl "http://example.com/v1/karma"
```

> Returned JSON:

```json
{
  "data": [
    {
      "id": 1,
      "giver_id": 1,
      "receiver_id": 2,
      "reason": "Helped me figure out some code!",
      "inserted_at": 1466737045,
      "updated_at": 1466737045
    }
  ]
}
```

Returns a list of all karma objects in the system.

### HTTP Request

`GET http://example.com/v1/karma[?filter=value]`

### Arguments

This endpoint supports a number of filters that can be applied to the end of the query:

### Returns

An object with a data property that contains an array of all karma objects in the system, ordered by ID. Each entry in the array is a separate karma object.

Attribute | Value | Description
--------- | ------- | -----------
since  | unix timestamp | Retrieve all karma created since <timestamp>.
given_by | user ID | Retrieve all karma that has been given by a certain user ID.
given_to | user ID | Retrieve all karma given to a certain user ID.





## Retrieve a karma object

> Example request:

```shell
curl "http://example.com/v1/karma/1"
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "reason": "Helped me figure out some code!",
    "type": "points",
    "amount": 1,
    "giver_id": 1,
    "receiver_id": 2,
    "inserted_at": 1466737045,
    "updated_at": 1466737045
  }
}
```

Returns a specific karma object.

### HTTP Request

`GET http://example.com/v1/karma/<karma_id>`

### Returns

Returns a karma object if a valid identifier was provided.





## Create karma

> Example request:

```shell
curl -v -X POST http://example.com/v1/karma \
     -H "Content-Type:application/json" \
     -d '{
           "karma": {
             "giver_id": 1,
             "receiver_id": 2,
             "reason": "Because user is awesome!"
           }
         }'
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "reason": "Because user is awesome!",
    "amount": 1,
    "type": "points",
    "giver_id": 1,
    "receiver_id": 2,
    "inserted_at": 1466737045,
    "updated_at": 1466737045
  }
}
```

Creates a new karma object.

### HTTP Request

`POST http://example.com/v1/karma`

### Returns

Returns the created karma object if the call succeeded.

### Arguments

Karma parameters must be all wrapped in a `karma` namespace before submitting.  Acceptable parameters are as follows:

Parameter | Description
--------- | -----------
giver_id (required) | User ID of user that is giving the karma.
receiver_id (required) | User ID of user that is receiving the karma.
reason | Reason karma was given.
amount | The number of karma you want to give. Defaults to 1.
type | The type of karma you want to give (e.g. points, unicorns, anything you want). Defaults to "points".





## Update karma

> Example request:

```shell
curl -v -X PUT http://example.com/v1/karma \
     -H "Content-Type:application/json" \
     -d '{
           "karma": {
             "giver_id": 2,
             "receiver_id": 3,
             "reason": "Changing the reason.",
             "type": "kitty kats",
             "amount": 400
           }
         }'
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "reason": "Changing the reason.",
    "amount": 400,
    "type": "kitty kats",
    "giver_id": 2,
    "receiver_id": 3,
    "inserted_at": 1466737045,
    "updated_at": 1466737045
  }
}
```

Updates an existing karma object.

### HTTP Request

`PUT http://example.com/v1/karma/<karma_id>`

### Returns

Returns the updated karma object if the call succeeded.

### Arguments

Karma parameters must be all wrapped in a `karma` namespace before submitting.  Acceptable parameters are as follows:

Parameter | Description
--------- | -----------
giver_id | User ID of user that is giving the karma.
receiver_id | User ID of user that is receiving the karma.
reason | Reason karma was given.
amount | The number of karma you want to give. Defaults to 1.
type | The type of karma you want to give. Defaults to "points".





## Delete karma

> Example request:

```shell
curl -v -X DELETE http://example.com/v1/karma/1 \
     -H "Content-Type:application/json"
```

> Returned JSON:

```json
{
  "data": {
    "id": 1,
    "reason": "Because user is awesome.",
    "amount": 1,
    "type": "points",
    "giver_id": 1,
    "receiver_id": 2,
    "inserted_at": 1466737045,
    "updated_at": 1466737045
  }
}
```

Deletes an existing karma object.

### HTTP Request

`DELETE http://example.com/v1/karma/<karma_id>`

### Returns

Returns the deleted karma object if the call succeeded.
