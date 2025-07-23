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

## Example usage

```go
expr, _ := datemath.Parse("now-15m")
fmt.Println(t.Time(datemath.WithNow(now)))
```

See [package documentation](https://pkg.go.dev/github.com/licaonfee/datemath) for usage and more examples.

## Extended expressions

### Bounded Week (`Bw`)

The `Bw` unit represents a bounded week, which always stays within a single month. When adding or subtracting bounded weeks:

* The minimum value returned is always the first day of the current month.
* The maximum value returned is always the first day of the next month.
* Calculations that would cross a month boundary are clamped to these limits.

This is useful for scenarios where week-based calculations should not cross into adjacent months.

#### Example

Suppose today is July 23, 2025:

```go
expr, _ := datemath.Parse("2025-07-23||+3Bw")
result := expr.Time()
fmt.Println(result.Format("2006-01-02")) // Output: 2025-08-01
```

In this example, adding one bounded week to July 23, 2025, returns August 1, 2025 (the first day of the next month), since the calculation would otherwise cross the month boundary.

## Development / Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).
