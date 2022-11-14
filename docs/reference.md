# 📕 Reference

## Authentication

Authentication is performed using the `Authorization` HTTP header in the format `Authorization: TOKEN_TYPE TOKEN`.

**Example Bearer Token Authorization Header:**

```json
{
  "Authorization": "Bearer you-access-token"
}
```

## Refresh Token

This token is generated when a new session is added, and is used to update the lifetime of the `access` token.
Please keep it in a safe place and do not show it to others, it may compromise the security of your account.

**Refresh token consists of:**

| Length   | Type   | Value          |
| -------- | ------ |:-------------: |
| 27 chars | KSUID  | Session Id.    |
| 27 chars | KSUID  | User Id.       |
| 33 chars | String | Token payload. |

**Example Refresh  Token**:

```json
"000000000000000000000000000.000000000000000000000000000.000000000000000000000000000000000"
```

**Implementation:**

- Go - [durudex/go-refresh](https://github.com/durudex/go-refresh)

## Secret Key

This key is generated and stored on the client and is used to ensure user security. It must be SHA256 hashed to
interact with the API.
