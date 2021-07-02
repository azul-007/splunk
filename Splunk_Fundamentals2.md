
# Module 3 

### Chart Command
Takes two clause statements: over and by
- The over clause tells splunk which fields you want on the X axis. The Y axis must always be numeric so that it can be charted.
- Any stats function can be used with the chart command.
- The by clause comes into play when you want to split your data by an additional field.
- Unlike the stats command, one only value can be specified after the "by" modifier when using the "over" clause.

The following example will search your web logs for any errors and tally how many times
each error occured on each host
```
index=web sourcetype=access_combined status > 299
product_name=*
| chart count over host by product_name limit=10
```

### Timechart Command
- Performs stats aggregations against time
- As with chart any stats function can be used with the chart command. The same applies for the "by" clause as in the chart command.
```
index=sales sourcetype=vendor_sales
| timechart sum(price) by product_name limit=0
```
