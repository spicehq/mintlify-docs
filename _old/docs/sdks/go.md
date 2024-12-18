---
description: Golang SDK for Spice.ai
---

# Go SDK

The [Go SDK](https://github.com/spiceai/gospice) `gospice` is the easiest way to query [Spice.ai](https://spice.ai) from Go.

It uses [Apache Arrow Flight](https://arrow.apache.org/docs/format/Flight.html) to efficiently stream data to the client and [Apache Arrow](https://arrow.apache.org/) Records as data frames.

GoDocs available at [pkg.go.dev/github.com/spiceai/gospice](https://pkg.go.dev/github.com/spiceai/gospice/v3).

### Requirements

* [Go 1.20](https://go.dev/doc/go1.20) (or later)

### Installation

Get the **gospice** package.

```bash
go get github.com/spiceai/gospice
```

### Usage

1\. Create a SpiceClient passing in your API key. Get your free API key at [spice.ai](https://spice.ai/).

```go
spice := gospice.NewSpiceClient()
defer spice.Close()
```

2\. Initialize the SpiceClient.

```go
if err := spice.Init("API Key"); err != nil {
    panic(fmt.Errorf("error initializing SpiceClient: %w", err))
}
```

3\. Execute a query and get back an Apache Arrow Reader.

```go
reader, err := spice.Query(context.Background(), "SELECT * FROM eth.recent_blocks ORDER BY number LIMIT 10")
if err != nil {
    panic(fmt.Errorf("error querying: %w", err))
}
defer reader.Release()
```

4\. Iterate through the reader to access the records.

```go
for reader.Next() {
    record := reader.Record()
    defer record.Release()
    fmt.Println(record)
}
```

### Example

Run `go run .` to execute a sample query and print the results to the console.

See [client\_test.go](https://github.com/spiceai/gospice/blob/trunk/client\_test.go) for examples on querying Ethereum and Polygon blocks.
