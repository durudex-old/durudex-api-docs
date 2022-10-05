# 📕 Introduction

## Errors

In case of incorrect requests or various server errors, an error will be returned to you.

```json
{
  "errors": [
    {
      "message": "Error Message",
      "extensions": {
        "code": "ERROR_CODE"
      }
    }
  ],
  "data": null
}
```

## Error Codes

Each of the status codes symbolizes the type of server error during the incoming request.

| Status Code                 | Description                                                               |
| :-------------------------: | ------------------------------------------------------------------------- |
| `SERVER_ERROR`              | A server error, most often caused by problems in the API Gateway.         |
| `INTERNAL_SERVER_ERROR`     | Internal server error caused by internal Durudex infrastructure problems. |
| `INVALID_ARGUMENT`          | In case of incorrect input arguments.                                     |
| `NOT_FOUND`                 | If no response is found for the specified arguments.                      |
| `ALREADY_EXISTS`            | If one of the specified arguments has been used by others before.         |
| `COMPLEXITY_LIMIT_EXCEEDED` | If the request complexity limit is exceeded.                              |
| `GRAPHQL_VALIDATION_FAILED` | When there are failed in GraphQL query validation.                        |

## Complexity

When sending heavy requests to the API, the server may return a `COMPLEXITY_LIMIT_EXCEEDED` error. This means that
the query complexity exceeds the specified limit and you need to simplify the query.

```json
{
  "errors": [
    {
      "message": "operation has complexity 1000, which exceeds the limit of 500",
      "extensions": {
        "code": "COMPLEXITY_LIMIT_EXCEEDED"
      }
    }
  ],
  "data": null
}
```

## Authentication

Authentication is performed using the `Authorization` HTTP header in the format `Authorization: TOKEN_TYPE TOKEN`.

```json
{
  "Authorization": "Bearer you-access-token"
}
```

## Refresh Token

This token is generated when a new session is added, and is used to update the lifetime of the `access` token.
Please keep it in a safe place and do not show it to others, it may compromise the security of your account.

**Refresh token consists of:**

| Part | Length   | Type   | Value          |
| :--: | :------: | :----: |:-------------: |
| 1    | 27 chars | KSUID  | Session Id.    |
| 2    | 27 chars | KSUID  | User Id.       |
| 3    | 33 chars | String | Token payload. |

> Note: Each part of the token is separated by a point.

**Fake token**:

```json
"000000000000000000000000000.000000000000000000000000000.000000000000000000000000000000000"
```

**Implementation:**

- Go - [durudex/go-refresh](https://github.com/durudex/go-refresh)

## Secret Key

This key is generated and stored on the client and is used to ensure user security. It must be SHA256 hashed to
interact with the API.

## Pagination

We provide flexible and powerful functionality for easy pagination.

The following arguments are used for pagination:

- `first` - Returns the first n elements from the list.
- `last` - Returns the last n elements from the list.
- `before` - Returns the elements in the list that come before the specified cursor.
- `after` - Returns the elements in the list that come after the specified cursor.

`nodes` - Returns a list of nodes.

```graphql
nodes {
  ...
}
```

`edges` - Returns a list of edges.

```graphql
edges {
  cursor
  node {
    ...
  }
}
```

`cursor` - This is a base64 encoded identifier.

`pageInfo` - Returns information about pagination.

- `startCursor` - Cursor for pagination backwards
- `endCursor` - Cursor for pagination forwards.

```graphql
pageInfo {
  startCursor
  endCursor
}
```
