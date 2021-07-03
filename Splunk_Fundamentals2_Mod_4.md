# Module 4

### IP Location

- Used to lookup and add location information such as the following to an event:

  * City *
  * Country *
  * Region *
  * Latitude *
  * Longitude *

```
index=security sourcetype=linux_secure action=success
| iplocation src_ip
```

### Geostsats

- Used to generate aggregate for map usage
- Uses the same functions as the stats command. The following returns data clustered by location
- The geostats command only accepts one argument for the by clause
```JavaScript
index=sales sourcetype=vendor_sales
| geostats latfield=VendorLatitude longfield=VendorLongitude count by product_name globallimit=4
```

- You can also look up geographical data to use with geostats using the iplocation command. You will use the lat and lon fields
- created by the iplocation

**This query shows you the locations where employees are accessing the servers**
```JavaScript
index=security sourcetype=linux_secure action=success
| iplocation src_ip
| geolocation latfield=lat longfield=lon count
```

### Choropleth Map
- Allows us to use shading to show relative metrics over predefined locations of a map
- In order to use choropleth you will need a KMZ file(geo_us_states or geo_countries), this file defines region boundaries
- To prepare our events for use in a choropleth, use the **geom** command
- The Geom command adds fields with geographical data structures matching polygons on your map
```
index=sales sourcetype=vendor_sales VendorID>=5000 AND VendorID<=5055
| stats count as Sales by VendorCountry
| geom geo_countries featureField=VendorCountry
```

### Trendline 

Computes moving averages of field values. The below is an example of how sales have trended over the last 7 days

```JavaScript
index=web sourcetype=access_combined action status=200 
| timechart sum(price) as sales
| trendline wma2(sales) as trend
```
The trendline command takes three arguments:
* trendtype - simple moving average (sma), exponential moving average (ema) or weighted moving average (wma)
* They compute the sum of data points over a period of time
* The wma and ema assign a heavier weighting to more current data points
* You need to define a period of time to use for computing the trend, this needs to been an integer 2<=10000
* In the example above I'm searching over the last 7 days, so a number of 2 will average the data points of every two days.
