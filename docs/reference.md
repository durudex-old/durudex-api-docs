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

The Refresh Token is generated by the internal authorization service during the creation of a new user session and
is used by the client for refreshing the access token. The token consists of three parts separated by point in the
`SESSION_ID.USER_ID.PAYLOAD` format.

- `SESSION_ID` - KSUID User session identifier.
- `USER_ID` - KSUID User identifier.
- `PAYLOAD` - Token payload that is used as a salt for the session payload hash.

**An example of Refresh Token:**

```json
"000000000000000000000000000.000000000000000000000000000.000000000000000000000000000000000"
```

**Implementation:**

- Go - [durudex/go-refresh](https://github.com/durudex/go-refresh)

## Secret Key

The secret key is used to protect the user account, it is used only to confirm the [Refresh Tokens](#refresh-token).
To use the maximum capabilities of the key, you can refuse to store key on the client, instead receive the key it
during the user's visit, even if an attacker gets your device, he will not be able to access the account without
this key. In order not to use raw data, the key should be hashed, it is recommended to use SHA3-256 hash or others
that will convert to a string of 64 characters.

**An example of using a secret key to create a session payload:**

```py
session_payload = hash_func(refresh_payload + secret_key)
```

Thus, we store neither the refresh token payload nor the secret key in the database. Even if someone receives the
payload of the session, they will not be able to access the account due to the pre-processing of the hash.
