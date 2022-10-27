# 😳 Go

## Install

You need to use this command and have [Go 1.18](https://go.dev) or higher installed to download.

```
go get github.com/durudex/durudex-go/sdk
```

## Default Client

The default client type is used for simple requests where authorization is not required.

```go
import "github.com/durudex/durudex-go/sdk"

func main() {
  client := sdk.NewClient(sdk.ClientConfig{
    Endpoint:      sdk.TestAPIEndpoint,
    TransportType: sdk.DefaultTransportType,
    Transport:     sdk.NewDefaultTransport(),
  })

  ...
}
```

**Client configuration:**

- `Endpoint` - Full url to Durudex GraphQL API. It is recommended to use prepared constants
from the sdk package.
- `TransportType` - A type of transport client, it is used to open certain functions, you
can learn more [here](#transport-type).
- `Transport` - This is a client transport implementation, for more functionality you can
implement your own version.

## Auth Client

This is a universal type of client that can be used in any case. It can automatically
refresh the access token.

```go
import "github.com/durudex/durudex-go/sdk"

func main() {
  client := sdk.NewClient(sdk.ClientConfig{
    Endpoint:      sdk.TestAPIEndpoint,
    TransportType: sdk.AuthTransportType,
    Transport:     sdk.NewAuthTransport(),
    AuthConfig: &sdk.AuthConfig{
      Refresh:    "refresh-token",
      Secret:     "client-secret-key",
      TokenType:  sdk.BearerTokenType,
      RefreshTTL: time.Minute * 15,
    },
  })

  ...
}
```

- `Refresh` - Full refresh token of the user.
- `Secret` - The client's secret key used in the session specified in the refresh token.
- `TokenType` - Authorization token type.
- `RefreshTTL` - The period of time after which the life of the access token will be
automatically renewed.

## Transport Type

The transport client type is used to expose certain functionality, such as authorization.

**DefaultTransportType**

This is a common type of client transport that is intended for simple requests where
no authorization is required.

**AuthTransportType**

This is a universal type of client that can be used in any case. It adds an HTTP authorization
header to each request. It can also automatically update the access token after the time
specified in the configuration.

## Custom Transport

Creating a custom transport adds new capabilities for the developer, such as custom error
handling, protocol switching, and more. To do this, you need to implement the methods of
the `sdk.Transport` interface.

**An example of creating custom transport:**

```go
type CustomTransport struct { ... }

func (*CustomTransport) RoundTrip(*http.Request) (*http.Response, error) { ... }

func (*CustomTransport) SetAccessToken(string) { ... }

func main() {
  client := sdk.NewClient(sdk.ClientConfig{
    Transport: &CustomTransport{},
    ...
  })

  ...
}
```

## Types Package

If you only need types, you can use a separate package that contains only them.

```
go get github.com/durudex/durudex-go/types
```

## Custom Request

To get the full functionality of GraphQL, you may need to create custom API queries.

**An example of creating a custom request:**

```go
import (
  ...

  "github.com/durudex/durudex-go/sdk"
  "github.com/Khan/genqlient/graphql"
)

type GetMeResponse struct {
  Me User `json:"me"`
}

type User struct {
  Username string `json:"username"`
}

func main() {
  client := sdk.NewClient( ... )

  req := &graphql.Request{
    Query:  "query GetMe { me { username } }",
    OpName: "GetMe",
  }

  var data GetMeResponse
  resp := &graphql.Response{Data: &data}

  client.MakeRequest(context.Background(), req, resp)
}
```

## Logging

You can use any package for logging, this can be done by implementing the methods
of the `sdk.Logger` interface. You then need to add this implementation to your
client configurations.

**An example of using a custom logger:**

```go
type CustomLogger struct{}

func (*CustomLogger) Debug(string) { ... }

func (*CustomLogger) Info(string) { ... }

func (*CustomLogger) Fatal(string) { ... }

func main() {
  client := sdk.NewClient(sdk.ClientConfig{
    Logger: &CustomLogger{}
    ...
  })

  ...
}
```
