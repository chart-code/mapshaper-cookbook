# mapshaper-cookbook

## Clip points in a CSV with a shapefile

This take a list [fires detected in Australia](https://blocks.roadtolarissa.com/1wheel/46874895034f5bded13c97097bf25a83), clips them to New South Wales and counts how many occur each day. 

```bash
mapshaper aus-fire/fire_nrt.csv \
  -clip aus-fire/NSW_STATE_POLYGON_shp.shp \
  -filter-fields acq_date \
  -dissolve acq_date calc='n = count()' \
  -o aus-fire/by-day-nsw.csv
```

The input data looks like this:

```csv
latitude,longitude,brightness,scan,track,acq_date,acq_time,satellite,instrument,confidence,version,bright_t31,frp,daynight
-18.439,145.293,331.3,1.3,1.1,2020-01-01,0050,Terra,MODIS,48,6.0NRT,307.5,22.5,D
-18.148,142.975,338.2,1,1,2020-01-01,0050,Terra,MODIS,65,6.0NRT,308.3,21.1,D
-18.16,142.993,337.3,1,1,2020-01-01,0050,Terra,MODIS,76,6.0NRT,302.5,23.4,D
```

and gets shrunk down to this:

```csv
acq_date,n
2020-01-01,3686
2020-01-02,4389
2020-01-03,4257
```