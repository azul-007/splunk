# Transactions

**Summary**

A transaction is any group of related events that span time

## Table of Contents

[Transaction Command](#transaction-command)

[Transaction Definition](#transaction-definition)

[Investigate with Transactions](#investigate-with-transactions)

[Transactions vs Stats](#transcations-vs-stats)





### Transaction Command
------------


The transaction command will allow you to search for an item that may be involved in multiple events.
The below query will search for all events with the clientip field. The command creates two fields: **duration** and **eventcount**.
The duration is the difference between the first and last event in the transaction. The evencount is the number of events in the transaction.

```JavaScript
index=web sourcetype=access_combined 
| transaction client 
| table clientip, action, product_name
```

The duration and eventcount fields can be use for statistics
```JavaScript
index=web sourcetype=access_combined 
| transaction client 
| timechart avg(duration)
```


### Transaction Definition
------------



### Investigate with Transactions
------------



### Transactions vs Stats
------------
