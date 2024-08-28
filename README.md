# datemath

[![GoDoc](https://godoc.org/github.com/timberio/go-datemath?status.svg)](https://pkg.go.dev/github.com/licaonfee/datemath)
[![Go Report Card](https://goreportcard.com/badge/github.com/timberio/go-datemath)](https://goreportcard.com/report/github.com/licaonfee/datemath)

This library provides support for parsing datemath expressions compatibly with [Elasticsearch datemath
expressions](https://www.elastic.co/guide/en/elasticsearch/reference/7.3/common-options.html#date-math). These are
useful for allowing users to specify, and for encoding, relative dates. Examples:

* `now+15m`: 15 minutes from now
* `now-1w+1d`: one day after on week ago
* `2015-05-05T00:00:00||+1M`: one month after 2019-05-05

These expressions will seem familiar if you have used Grafana or Kibana.

Example usage:

```go
expr, _ := datemath.Parse("now-15m")
fmt.Println(t.Time(datemath.WithNow(now)))
```

See [package documentation](https://pkg.go.dev/github.com/licaonfee/datemath) for usage and more examples.

## Development / Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).
