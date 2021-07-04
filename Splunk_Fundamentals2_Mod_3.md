
# Module 3 

### Chart Command
Takes two clause statements: over and by
- The over clause tells splunk which fields you want on the X axis. The Y axis must always be numeric so that it can be charted.
- Any stats function can be used with the chart command.
- The by clause comes into play when you want to split your data by an additional field.
- Unlike the stats command, one only value can be specified after the "by" modifier when using the "over" clause.

The following example will search your web logs for any errors and tally how many times
each error occured on each host
```JavaScript
index=web sourcetype=access_combined status > 299
product_name=*
| chart count over host by product_name limit=10
```

### Timechart Command
- Performs stats aggregations against time
- As with chart any stats function can be used with the chart command. The same applies for the "by" clause as in the chart command.
```JavaScript
index=sales sourcetype=vendor_sales
| timechart sum(price) by product_name limit=0
```

To change the span of the time of the cluster, you can use an arguement of span with the time to group by.
```JavaScript
index=sales sourcetype=vendor_sales
| timechart span=12hr sum(price) by product_name limit=0
```

### Timewrap Command
Compares data over specific time periods, such as comparing this weeks game sales to last weeks games sales.
Say you're comparing the sales for "Dream Crusher" over the last 27 days. To use the **timewrap** command, specify
a period of time from the results of the timechart command. Splunk will format the results, so every increment of that
period is a different is a different series.

The timewrap value of 7d, splits the 27 day time range into four segments
```JavaScript
index=sales sourcetype=vendor_sales product_name="Dream Crusher"
| timechart span=1d sum(price) by product_name
| timewrap 7d 
| rename _time as Day
| eval Day = strftime(Dy, "%A")
```
