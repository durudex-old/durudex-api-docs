# 🌐 GraphQL

## Pagination

We provide flexible and powerful functionality for easy pagination.

**The following arguments are used for pagination:**

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
