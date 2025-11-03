---
layout: page
---

# `user` resource

Base endpoint:

```shell

{server_url}/users
```

Contains information about the users of the service.

A user resource describes the owners of the tasks in the service.
Before you can create a `task` resource in the service,
you must create the 'user' resource to assign to the `task`.

Learn more about the [task resource](task.md).

## Resource properties

Sample `user` resource

```js

{
    "last_name": "Smith",
    "first_name": "Ferdinand",
    "email": "f.smith@example.com",
    "id": 1
}
```

| Property name | Type | Description |
| ------------- | ----------- | ----------- |
| `last_name` | string | The user's last name |
| `first_name` | string | The user's first name |
| `email` | string | The user's email address |
| `id` | number | The user's unique record ID |

## Read operations

* [Get all users](users-get-all-users.md)
* [Get users by ID](users-get-user-by-id.md)
