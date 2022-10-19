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

## Sign Up

You'll need the following information to create a new user account:

- `username` - Unique username.
- `password` - Strong password.
- `email` - User's email address.
- `code` - E-mail confirmation code.
- `secret` - Client secret key.

You can learn how to get the verification code [here](#get-verification-code).

```graphql
mutation {
  signUp(input: {
    username: "example",
    email: "example@durudex.com",
    password: "qwerty",
    code: "123456",
    secret: "secret-key"
  }) {
    access
    refresh
  }
}
```

## Sign In

You will need your credentials to sign in to your account:

- `username` - Your account name.
- `password` - Your account password.
- `secret` - Client secret key.

```graphql
mutation {
  signIn(input: {
    username: "example",
    password: "qwerty",
    secret: "secret-key"
  }) {
    access
    refresh
  }
}
```

## Refresh Token

To refresh the life of your access token, you need to perform the following request:

```graphql
mutation {
  refreshToken(input: {
    refresh: "refresh-token",
    secret: "secret-key"
  })
}
```

## Forgot Password 

If you need to reset your user password, you will need the following information:

- `email` - User's email address.
- `password` - New strong user password.
- `code` - Code to confirm of the e-mail.

You can learn how to get the verification code [here](#get-verification-code).

```graphql
mutation {
  forgotPassword(input: {
    email: "example@durudex.com",
    password: "qwerty",
    code: "123456"
  })
}
```

## Get Verification Code

If you need to get a verification code, you will need the following information:

- `email` - User's email address.

```graphql
mutation {
  createVerifyEmailCode(email: "example@durudex.com")
}
```

A message with a confirmation code will be sent to the indicated email. Use this code as soon
as possible, it doesn't last long.

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
