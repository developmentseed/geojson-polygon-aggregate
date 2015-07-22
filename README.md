# geojson-polygon-aggregate

Aggregate properties of GeoJSON polygons, grouped by another set of polygons

## Install

```
npm install geojson-polygon-aggregate
```


## Usage

```
var aggregate = require('geojson-polygon-aggregate')
var groups = { /* geojson FeatureCollection of polygons */ }
var data = {
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "something": 1000,
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              124.78134155273439,
              6.676883507787369
            ],
            [
              124.69207763671875,
              6.626413768432949
            ],
            [
              124.65637207031251,
              6.477702768909363
            ],
            [
              124.69894409179686,
              6.324853151663241
            ],
            [
              124.7113037109375,
              6.234759816458916
            ],
            [
              124.80880737304686,
              6.206090498573885
            ],
            [
              124.82666015624999,
              6.39582473299521
            ],
            [
              124.97085571289062,
              6.2361249830392875
            ],
            [
              125.0848388671875,
              6.35897532723566
            ],
            [
              125.09857177734375,
              6.229299114609287
            ],
            [
              125.13427734374999,
              6.495441264930553
            ],
            [
              124.97909545898436,
              6.526823225180418
            ],
            [
              125.09445190429688,
              6.655059391963758
            ],
            [
              124.78134155273439,
              6.676883507787369
            ]
          ]
        ]
      }
    },
    {
      "type": "Feature",
      "properties": {
        "something": 729
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              124.65774536132812,
              6.68097542126577
            ],
            [
              124.6783447265625,
              6.211551441519991
            ],
            [
              125.13290405273438,
              6.219742749707111
            ],
            [
              125.12466430664064,
              6.682339384819373
            ],
            [
              124.69619750976562,
              6.690523086226235
            ],
            [
              124.69482421875,
              6.712345619186976
            ],
            [
              125.14938354492188,
              6.704162283788004
            ],
            [
              125.15350341796874,
              6.1938031700764045
            ],
            [
              124.65774536132812,
              6.1883420433598335
            ],
            [
              124.63027954101562,
              6.683703344568804
            ],
            [
              124.65774536132812,
              6.68097542126577
            ]
          ]
        ]
      }
    }
  ]
}

var result = aggregate(groups, data, {
  'something': aggregate.sum('something'),
  'something-area-weighted': aggregate.sum('something'),
  'area': aggregate.totalArea(),
  'count': aggregate.count(),
  'arbitraryProperty': function (memo, feature) {
    // the aggregations above are provided for convenience, but you can
    // do whatever you want here. `memo` is the previous return value
    // of this function, or groups.properties['arbitraryProperty'] on the
    // first iteration.
    return (memo || 1) * feature.properties['something']
  }
})
```


