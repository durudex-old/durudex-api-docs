# 🙂 User

## User Structure

| Field       | Type    | Description           |
| :---------: | :-----: | --------------------- |
| `id`        | KSUID   | User id.              |
| `username`  | String  | Unique username.      |
| `verified`  | Boolean | User verified status. |
| `avatarUrl` | String  | User avatar url.      |

**Example User:**

```json
{
  "id": "000000000000000000000000000",
  "username": "example",
  "verified": false,
  "avatarUrl": "000000000000000000000000000.png"
}
```

## Get User

You can get all the public information about the user.

```graphql
query {
  user(id: "user-id") {
    username
    avatarUrl
    ...
  }
}
```

## Get Yourself

You can get information about yourself, this requires authorization.

```graphql
query {
  me {
    username
    avatarUrl
    ...
  }
}
```
