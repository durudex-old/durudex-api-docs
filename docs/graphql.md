# 🌐 GraphQL

## Error Message

In case of incorrect requests or various server errors, an error will be returned to you.

**An example of an error:**

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
| `SERVER_ERROR`              | A server error, most often caused by errors in the API Gateway.           |
| `INTERNAL_SERVER_ERROR`     | Internal server error caused by internal Durudex infrastructure errors.   |
| `INVALID_ARGUMENT`          | In case of incorrect input arguments.                                     |
| `NOT_FOUND`                 | If no response is found for the specified arguments.                      |
| `ALREADY_EXISTS`            | If one of the specified arguments has been used by others before.         |
| `COMPLEXITY_LIMIT_EXCEEDED` | If the request complexity limit is exceeded.                              |
| `GRAPHQL_VALIDATION_FAILED` | When there are failed in GraphQL query validation.                        |

## Pagination

We provide flexible and powerful functionality for easy pagination, you can learn more [here](https://relay.dev/graphql/connections.htm).

## Complexity

When sending heavy requests to the API, the server may return a `COMPLEXITY_LIMIT_EXCEEDED` error. This means that
the query complexity exceeds the specified limit and you need to simplify the query.

**An example of an error:**

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
