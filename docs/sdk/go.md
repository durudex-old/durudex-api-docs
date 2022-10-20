# 😳 Go

## Install

You need to use this command and have [Go 1.18](https://go.dev) or higher installed to download.

```
go get github.com/durudex/durudex-go/sdk
```

## Default Client

The default client type is used for simple requests where authorization is not required.

```go
package main

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
package main

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

This is a universal type of client transport that is used for requests that require
authorization, it can also be used for simple requests.
