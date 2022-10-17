# 📄 Post

## Post Structure

| Field         | Type      | Description            |
| :-----------: | :-------: | ---------------------- |
| `id`          | KSUID     | Post id.               |
| `author`      | User      | Post author.           |
| `text`        | String    | Post text.             |
| `updatedAt`   | Timestamp | Post updated date.     |
| `attachments` | []String  | Post attachments list. |

**Example Session:**

```json
{
  "id": "000000000000000000000000000",
  "author": {
    "id": "000000000000000000000000000"
  },
  "text": "Hello Durudex!",
  "updatedAt": "0000-00-00T00:00:00Z",
  "attachments": [
    "durudex.png"
  ]
}
```

## Create post

You need to be authorized to create a new post. You will also need the following information:

- `text` - The main text of your post.

```graphql
mutation {
  createPost(input: {text: "Hello Durudex!"})
}
```

## Delete post

You need to be authorized to delete your post.

```graphql
mutation {
  deletePost(id: "post-id")
}
```

## Update Post

You need to be authorized to update your post.

```graphql
mutation {
  updatePost(input: {
    id: "post-id",
    text: "Durudex to the moon 🚀"
  })
}
```

## Get Post

Request to get a post using id:

```graphql
query {
  post(id: "post-id") {
    text
    author {
      id
    }
  }
}
```

## Get User Posts

Request to get a list of user posts:

```graphql
query {
  user(id: "user-id") {
    posts(first: 10) {
      nodes {
        id
        text
        attachments
      }
    }
  }
}
```
