# Tags and Event Types

- Tags allow you to designate descriptive names for key-value pairs
- Tags enable you to search for events that contain particular field values


## Table of Contents

[Creating Tags](#creating-tags)

[Event Type](#event-type)


[Event Types vs Saved Reports](#event-types-vs-saved-reports)




### Creating Tags
------------

Create tags by clicking on an event information link and clicking the action link for the field value pair we want to tag.
An 'Edit Tags' link will appear. Click it and we get the 'Create Tags' dialog box. In the Field Value input box you will see the field you selected. Under it is the 'Tags' input box where you will name your tag. Your tags will be displayed next to the field value.

Tag values are case sensitive in your searches. Manage your tags by going to the Settings menu -> Tags. You can list tags by field value pair, tag name or by unique tag objects.


### Event Type
------------

Event types allow you to categorize events based on search terms

**Event Type from Search**

Say you've been approached by the ButterCup Games sales team. They would like to track all of the online purchases made by product type. You can create event types to help simplify their searches and give them quick visual feedback.

The below example searches for all purchases made for games in the strategy category

```JavaScript
index=web sourcetype=access_combined action=purchase categoryId=STRATEGY
```

Save the query as an event type. Enter a name for the event type. Fill out the fields you wish and run the query again with your new event type value.

```JavaScript
index=web sourcetype=access_combined action=purchase categoryId=STRATEGY
eventtype=purchase_strategy
```

**Event Type Builder**

From an event's information link, select 'Build Event Type' from the event action menu. 


### Event Types vs Saved Reports
------------

So when should you use an event type or create a saved report?

Event Types

- categorize events based on search string
- use tags to organize
- "eventtype" field within a search string
- DOES NOT INCLUDE A TIME RANGE

Saved Reports

- Used when the search criteria will not change
- When you need to include the time range and format
- Share with other Splunk users
- Add to dashboards
