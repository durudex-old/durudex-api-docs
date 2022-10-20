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

This is a universal type of client that can be used in any case. It adds an http authorization
header to each request. It can also automatically update the access token after the time
specified in the configuration.

## Types Package

If you only need types, you can use a separate package that contains only them.

```
go get github.com/durudex/durudex-go/types
```

## Logging

You can use any package for logging, this can be done by implementing the methods
of the `sdk.Logger` interface. You then need to add this implementation to your
client configurations.

**An example of using a custom logger:**

```go
type CustomLogger struct{}

func (l *CustomLogger) Debug(msg string) { ... }

func (l *CustomLogger) Info(msg string) { ... }

func (l *CustomLogger) Fatal(msg string) { ... }

func main() {
	client := sdk.NewClient(sdk.ClientConfig{
		Logger: &CustomLogger{}
		...
	})

	...
}
```
