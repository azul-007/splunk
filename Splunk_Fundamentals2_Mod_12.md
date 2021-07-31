# Worflow Actions

Workflow actions let us create links within events interact with external resources or narrow down your search. 

They use the HTTP GET and POST methods to pass information to external sources or can pass information back to splunk to perform a secondary search.



## Table of Contents

[Create GET](#create-get)

[Create POST](#create-post)

[Create search](#create-search)


### Create GET
------------

To create a new workflow action, go to Settings -> Fields -> Workflow actions and select Add New

When filling out the fields in the workflow, you can include the field name in the Label by enclosing it in dollar signs: $example$.

Next enter the fields to apply the action to. You may also choose which event types to apply it to. Leave it blank to apply to all events.

![Screen Shot 2021-07-30 at 10 22 28 PM](https://user-images.githubusercontent.com/15880042/127725879-bc643a68-552b-491a-b1cc-75f1993ba94f.png)

To test, rerun your search, select an event, select Event Actions and observe the GetWhoIs for IPAddress link

![Screen Shot 2021-07-30 at 10 24 00 PM](https://user-images.githubusercontent.com/15880042/127725938-3aaf1482-18cd-4352-b352-fbb9d9f24c02.png)




### Create POST
------------

Say you wanted to create tickts from form input through Splunk. This is where workflow actions can come in handy. They allow you to send pre-filled
forms or communicate with an API.

To create a POST, follow the same steps as with GET..the major difference being the POST arguments you would liked defined under 
'Link configuration'.

![Screen Shot 2021-07-30 at 10 38 01 PM](https://user-images.githubusercontent.com/15880042/127726194-abb6b411-5368-41b5-a7ef-4f394134e695.png)






### Create search
------------

Say you wanted to take your failed password example from before, you can add an action where you can search for other events where the IP might appear.

Follow the same, exact same steps as the GET and POST, except this time select 'search' for Action type.

Enter the search string to use when the action is launched. 

