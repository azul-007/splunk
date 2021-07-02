
# Module 3 

### Chart Command
Takes two clause statements: over and by
- The over clause tells splunk which fields you want on the X axis. The Y axis must always be numeric so that it can be charted.
- Any stats function can be used with the chart command.
- The by clause comes into play when you want to split your data by an additional field.

The following example will search your web logs for any errors and tally how many times
each error occurs.
```
index=web sourcetype=access_combined status > 299
product_name=*
| chart count over host by product_name 
```

### Timechart Command
