# 📄 Post

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

## Update post

You need to be authorized to update your post.

```graphql
mutation {
  updatePost(input: {
    id: "post-id",
    text: "Durudex to the moon 🚀"
  })
}
```

## Get post

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

## Get user posts

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
