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

The transaction command includes some definitions options. The most common being maxspan, maxpause, startswith and endswith.

- **maxspan:**  allows you to set the total time between the earliest and latest events.
- **maxpause:**  is the maximum total time allowed between events. 
- **startswith:**  allows forming transactions starting with specified terms, field values, evaluations
- **endswith:** allows forming transactions ending with specified terms, field values, evaluations

The following shows a query depicting transactions that occur when a customer adds an item to their shopping cart and ends
when they purchase the item.

```JavaScript
index=web sourcetype=access_combined 
| transaction client startswith="addtocart" endswith="purchase"
| table clientip, action, product_name
```

### Investigate with Transactions
------------
Say you wanted to search what emails were rejected by your security appliances, you could search for the term "reject" for the 
sourcetype. But you also want to see the IP of the sender and the actin taken by the mail server after the rejection. You can pipe
the sourcetype into a transaction that occurs on multiple fields, use a search command on those transactions to see all events that
happen around that rejection. 

```JavaScript
index=network sourcetype=cisco_esa
| transaction mid dcid icid
| search REJECT
```

### Transactions vs Stats
------------

When should you use transactions as opposed to stats and vice versa?

Use transactions when:

1) You need to see events correlated together
2) Use when events  need to be grouped on start and end values

Use stats when:

1) Want to see results of a calculation
2) Or when you need to group events on a field value

Stats command is faster and more efficient.
