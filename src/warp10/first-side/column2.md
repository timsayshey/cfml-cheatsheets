# Bucketizer











Syntaxe: __[ [GTS] *bucketizer* *lastbucket* *bucketspan* *bucketcount* ] BUCKETIZE__

Ex: *return 100 meaning datapoints from the previous GeoTimeSeries®*
```
[ SWAP bucketizer.mean 0 0 100 ] BUCKETIZE
```

# Reducer

















Syntaxe: __[ [GTS]...[GTS] [*labels*] *reducer* ] REDUCE__

Ex: *return a sum of aggregated GeoTimeSerie® from the previous GeoTimeSerie®*
```
[ SWAP [ 'label1'] reducer.sum ] REDUCE
```
