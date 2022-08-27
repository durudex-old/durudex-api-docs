# 🗿 Test API

You can use our test API for development, which provides full functionality of the main API. The data that the 
server returns to you is not real, each time the data will be different.

## Start

If you want to assemble a test application yourself, then you need:

1) Downloading the source code and creating the necessary files.

```shell
# Clone repository.
git clone https://github.com/durudex/durudex-test-api.git

# Change directory.
cd durudex-test-api

# Create environment file.
touch .env
```

2) Environment settings (edit the `.env` file).

```shell
# Debug mode.
DEBUG=false

# Config variables:
CONFIG_PATH=configs/dev

# Auth variables:
JWT_SIGNING_KEY=
```

3) Use `make` to run or `make build` to build application.

You can now navigate to [localhost:8000](localhost:8000) to the query editor.

## Usage

To use, you need to add `/query` to your url and send only POST requests.

## Docker container

You can also use a ready-made docker container - [durudex/durudex-test-api](https://hub.docker.com/r/durudex/durudex-test-api).

## Configuration

To configure the test API, you need to go to `configs/` and create or edit an existing one
configuration file.

```yaml
http:
  host: "api.test.durudex.com"
  port: 8000
  name: "Durudex Test API"
  cors:
    enable: true
    allow-origins: "*"
    allow-methods: "GET,POST"
    allow-headers: "*"

graphql:
  complexity-limit: 500

auth:
  ttl: 15m # JWT access token ttl
```

To change the configuration file, you need to change `CONFIG_PATH=you-path` in `.env` file.
