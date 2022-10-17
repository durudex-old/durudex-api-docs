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
