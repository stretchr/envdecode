# envdecode #

`envdecode` is a Go package for populating structs from environment
variables.

`envdecode` uses struct tags to map environment variables to fields,
allowing you you use any names you want for environment variables.
`envdecode` will recurse into nested structs, including pointers to
nested structs, but it will not allocate new pointers to structs.

## API ##

Define a struct with `env` struct tags:

```go
type Config struct {
    Hostname  string `env:"SERVER_HOSTNAME"`
    Port      uint16 `env:"SERVER_PORT"`

    AWS struct {
        ID     string `env:"AWS_ACCESS_KEY_ID"`
        Secret string `env:"AWS_SECRET_ACCESS_KEY"`
    }
}
```

Then call `envdecode.Decode`:

```go
var cfg Config
err := envdecode.Decode(&cfg)
```