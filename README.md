# SQL Setting Benchmark in Go

This is a benchmark of adjustable setting of `database/sql` module in Go.

## Settings
- Max Open Connections (Maximum number of in-use and idle connections).
- Max Idle Connections (Maximum number of idle connections).
- Connectinon Max Lifetime (Maximum duration of a connection can be reused).

## Preparation
Create `isbns` table in the database.

```
CREATE TABLE `isbns` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `isbn` varchar(255) NOT NULL,
  PRIMARY KEY (`id`)
);
```

## Benchmark
Run benchmarking with `go test` command.

```
# run benchmarking 5 times and show memory allocation
go test -bench=. -count 5 -benchmem
```

## Result
```
➜ go test -bench=. -count 5 -benchmem
goos: darwin
goarch: amd64
pkg: github.com/madeindra/go-pq-bench
cpu: Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz
BenchmarkMaxOpenConns1-12                            405           3401761 ns/op             847 B/op         14 allocs/op
BenchmarkMaxOpenConns1-12                            619           1768446 ns/op             773 B/op         13 allocs/op
BenchmarkMaxOpenConns1-12                            682           1865374 ns/op             759 B/op         13 allocs/op
BenchmarkMaxOpenConns1-12                            705           1540964 ns/op             747 B/op         13 allocs/op
BenchmarkMaxOpenConns1-12                            666           1623889 ns/op             757 B/op         13 allocs/op
BenchmarkMaxOpenConns2-12                           1089           1008782 ns/op             758 B/op         13 allocs/op
BenchmarkMaxOpenConns2-12                           1029            990478 ns/op             763 B/op         13 allocs/op
BenchmarkMaxOpenConns2-12                            934           1091029 ns/op             769 B/op         13 allocs/op
BenchmarkMaxOpenConns2-12                           1113           1235899 ns/op             761 B/op         13 allocs/op
BenchmarkMaxOpenConns2-12                            864           1232235 ns/op             767 B/op         13 allocs/op
BenchmarkMaxOpenConns5-12                           1668            694855 ns/op             773 B/op         13 allocs/op
BenchmarkMaxOpenConns5-12                           1683            669891 ns/op             778 B/op         13 allocs/op
BenchmarkMaxOpenConns5-12                           1591            741343 ns/op             774 B/op         13 allocs/op
BenchmarkMaxOpenConns5-12                           1756            710746 ns/op             775 B/op         13 allocs/op
BenchmarkMaxOpenConns5-12                           1693            677212 ns/op             771 B/op         13 allocs/op
BenchmarkMaxOpenConns10-12                          2030            621007 ns/op             816 B/op         14 allocs/op
BenchmarkMaxOpenConns10-12                          1981            565175 ns/op             811 B/op         14 allocs/op
BenchmarkMaxOpenConns10-12                          2001            685375 ns/op             814 B/op         14 allocs/op
BenchmarkMaxOpenConns10-12                          1591            699425 ns/op             837 B/op         14 allocs/op
BenchmarkMaxOpenConns10-12                          1318            776849 ns/op             864 B/op         15 allocs/op
BenchmarkMaxOpenConnsUnlimited-12                   1189            953062 ns/op             906 B/op         15 allocs/op
BenchmarkMaxOpenConnsUnlimited-12                   1098           1069478 ns/op             952 B/op         15 allocs/op
BenchmarkMaxOpenConnsUnlimited-12                   1088           1171519 ns/op             935 B/op         15 allocs/op
BenchmarkMaxOpenConnsUnlimited-12                   1017           1272588 ns/op             988 B/op         16 allocs/op
BenchmarkMaxOpenConnsUnlimited-12                    843           1409341 ns/op             991 B/op         16 allocs/op
BenchmarkMaxIdleConnsNone-12                          94          12380048 ns/op           20307 B/op        281 allocs/op
BenchmarkMaxIdleConnsNone-12                          81          16118709 ns/op           20313 B/op        282 allocs/op
BenchmarkMaxIdleConnsNone-12                          69          15146620 ns/op           20295 B/op        281 allocs/op
BenchmarkMaxIdleConnsNone-12                          76          15275019 ns/op           20286 B/op        281 allocs/op
BenchmarkMaxIdleConnsNone-12                          78          13981676 ns/op           20237 B/op        280 allocs/op
BenchmarkMaxIdleConns1-12                            456           2708686 ns/op            2187 B/op         32 allocs/op
BenchmarkMaxIdleConns1-12                            451           3166790 ns/op            2675 B/op         39 allocs/op
BenchmarkMaxIdleConns1-12                            433           2825717 ns/op            2542 B/op         37 allocs/op
BenchmarkMaxIdleConns1-12                            428           2813568 ns/op            2387 B/op         35 allocs/op
BenchmarkMaxIdleConns1-12                            351           3268909 ns/op            2609 B/op         38 allocs/op
BenchmarkMaxIdleConns2-12                            391           2776694 ns/op            1495 B/op         23 allocs/op
BenchmarkMaxIdleConns2-12                            532           2253007 ns/op            1371 B/op         21 allocs/op
BenchmarkMaxIdleConns2-12                            574           2290327 ns/op            1108 B/op         17 allocs/op
BenchmarkMaxIdleConns2-12                            547           2024549 ns/op            1131 B/op         18 allocs/op
BenchmarkMaxIdleConns2-12                            501           2231602 ns/op            1257 B/op         20 allocs/op
BenchmarkMaxIdleConns5-12                            495           2134667 ns/op            1072 B/op         17 allocs/op
BenchmarkMaxIdleConns5-12                            570           2346152 ns/op            1007 B/op         16 allocs/op
BenchmarkMaxIdleConns5-12                            543           2149044 ns/op            1027 B/op         16 allocs/op
BenchmarkMaxIdleConns5-12                            650           1983955 ns/op             954 B/op         15 allocs/op
BenchmarkMaxIdleConns5-12                            427           2414261 ns/op            1142 B/op         18 allocs/op
BenchmarkMaxIdleConns10-12                           428           3279860 ns/op            1146 B/op         18 allocs/op
BenchmarkMaxIdleConns10-12                           530           1943626 ns/op            1037 B/op         17 allocs/op
BenchmarkMaxIdleConns10-12                           596           1867738 ns/op             992 B/op         16 allocs/op
BenchmarkMaxIdleConns10-12                           696           1781522 ns/op             933 B/op         15 allocs/op
BenchmarkMaxIdleConns10-12                           657           1638313 ns/op             955 B/op         15 allocs/op
BenchmarkConnMaxLifetimeUnlimited-12                 734           1612288 ns/op            1152 B/op         18 allocs/op
BenchmarkConnMaxLifetimeUnlimited-12                 781           1538914 ns/op            1067 B/op         17 allocs/op
BenchmarkConnMaxLifetimeUnlimited-12                 775           1390734 ns/op            1055 B/op         17 allocs/op
BenchmarkConnMaxLifetimeUnlimited-12                 760           1319875 ns/op            1108 B/op         17 allocs/op
BenchmarkConnMaxLifetimeUnlimited-12                1081           1123511 ns/op             974 B/op         16 allocs/op
BenchmarkConnMaxLifetime1000-12                     1016           1166163 ns/op            1057 B/op         17 allocs/op
BenchmarkConnMaxLifetime1000-12                     1029           1137873 ns/op            1069 B/op         17 allocs/op
BenchmarkConnMaxLifetime1000-12                     1120           1121421 ns/op            1067 B/op         17 allocs/op
BenchmarkConnMaxLifetime1000-12                     1338            966277 ns/op             989 B/op         16 allocs/op
BenchmarkConnMaxLifetime1000-12                     1162            870328 ns/op             999 B/op         16 allocs/op
BenchmarkConnMaxLifetime500-12                      1443            838370 ns/op            1043 B/op         17 allocs/op
BenchmarkConnMaxLifetime500-12                      1528            714732 ns/op             979 B/op         16 allocs/op
BenchmarkConnMaxLifetime500-12                      1351            772374 ns/op            1085 B/op         17 allocs/op
BenchmarkConnMaxLifetime500-12                      1465            764420 ns/op            1010 B/op         16 allocs/op
BenchmarkConnMaxLifetime500-12                      1620            712611 ns/op            1006 B/op         16 allocs/op
BenchmarkConnMaxLifetime200-12                      1310            877257 ns/op            1526 B/op         23 allocs/op
BenchmarkConnMaxLifetime200-12                      1393            857531 ns/op            1485 B/op         23 allocs/op
BenchmarkConnMaxLifetime200-12                      1353            893293 ns/op            1513 B/op         23 allocs/op
BenchmarkConnMaxLifetime200-12                      1237            924887 ns/op            1536 B/op         23 allocs/op
BenchmarkConnMaxLifetime200-12                      1364            912975 ns/op            1520 B/op         23 allocs/op
BenchmarkConnMaxLifetime100-12                      1032           1231024 ns/op            2348 B/op         35 allocs/op
BenchmarkConnMaxLifetime100-12                       955           1201477 ns/op            2307 B/op         34 allocs/op
BenchmarkConnMaxLifetime100-12                       769           1354186 ns/op            2490 B/op         37 allocs/op
BenchmarkConnMaxLifetime100-12                       889           1191274 ns/op            2347 B/op         35 allocs/op
BenchmarkConnMaxLifetime100-12                      1004           1281425 ns/op            2421 B/op         36 allocs/op
PASS
ok      github.com/madeindra/go-pq-bench        164.639s
```

Let's see the first line:
```
BenchmarkMaxOpenConns1-12                            405           3401761 ns/op             847 B/op         14 allocs/op
```

This is how you read the reports above:
- `BenchmarkMaxOpenConns1-12` means that the benchmark is running `BenchmarkMaxOpenConns1` function that has `MaxOpenConns` set to `1` and the number after the `-` is the number of CPUs used.
- `405` is the number of iterations that the benchmark has run for that function.
- `3401761 ns/op`is the average amount of time taken for each iteration to complete.
- `847 B/op` is the average number of memory allocated per iteration.
- `14 allocs/op` is the average number of allocations per iteration.

### Reference
- Alex Edwards - [Configuring sql.DB for Better Performance](https://www.alexedwards.net/blog/configuring-sqldb).
- Logrocket - [Benchmarking in Golang: Improving function performance](https://blog.logrocket.com/benchmarking-golang-improve-function-performance/).