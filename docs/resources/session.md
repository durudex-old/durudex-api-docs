# ⏳ Session

## Session Structure

| Field       | Type      | Description               |
| :---------: | :-------: | ------------------------- |
| `id`        | KSUID     | Session id.               |
| `userId`    | KSUID     | User session owner id.    |
| `ip`        | String    | Session owner ip address. |
| `expiresIn` | Timestamp | Session expires in.       |

**Example Session:**

```json
{
    "id": "000000000000000000000000000",
    "userId": "000000000000000000000000000",
    "ip": "127.0.0.1",
    "expiresIn": "0000-00-00T00:00:00Z"
}
```

## Get Session

Request to get a session using id:

```graphql
query {
  session(id: "session-id") {
    id
    userId
    ip
    expiresIn
  }
}
```

## Get Sessions

Request to get a sessions:

```graphql
query {
  sessions(last: 10) {
    nodes {
      id
      userId
      ip
      expiresIn
    }
  }
}
```
