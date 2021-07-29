# Macros

Macros are reusable search strings or portions of search strings that can be resued in multiple places within Splunk. They are useful for frequent searches 
with complicated search syntax. 

- They allow you to store entire search strings including pipes and eval statements
- They are time range independent, allowing the time range to be selected at search time
- Can pass arguments to the search

## Table of Contents

[Create Macro](#create-macro)

[Macro Argument](#marcro-argument)

[Multiple Arguments](#Multiple-Arguments)

[Expanding Search](#expanding-search)

### Create Macro
------------

The following query sums all the sales by vendor and then passes those to an eval command that formts the totals to display in US dollar amounts.

```JavaScript
index=sales sourcetype=vendor_sales
| stats sum(sale_price) as total_sales by Vendor
| eval total_sales = "$" tostring(round(total_sales,2),"commas")
```

To save time from having to enter the eval command each time you can create a macro. Go to Settings -> Advanced Search -> Search macros

For the Destination App leave it as 'search'. Select a name for your macro. The definition will be the eval statement used to make your conversion earlier. And save.

![macro](https://user-images.githubusercontent.com/15880042/127416123-495d0fc4-2117-4176-b307-54838346d207.png)

Test by piping search into the macro instead of the eval command. To use the macro, surround it with the back tick characters like so 'convertUSD'

```JavaScript
index=sales sourcetype=vendor_sales
| stats sum(sale_price) as total_sales by Vendor
| `convertUSD`
```



### Macro Argument
------------

The goal of a macro is to always make it as resuable as possible. With the current definition, you would always need to pass the currency to convert as total_sales.

We're going to change the definition to accept an argument by adding the name of the argument surrounded by dollar signs. You have replaced the static total_sales field
allowing the macro to receive and return the converted values using any field name.

Add the argument name to the arguments field and hit save. Test your macro by adding the total sales field to it.

![Screen Shot 2021-07-28 at 9 24 25 PM](https://user-images.githubusercontent.com/15880042/127417235-23540506-51c9-4916-949f-1ff5f0dc3cb1.png)

The macro can now be passed with any number that you want displayed in US currency.

```JavaScript
index=sales sourcetype=vendor_sales
| stats sum(sale_price) as Average_Price by product_name
| `convertUSD("Average_Price")`
```



### Multiple Arguments
------------

Since you are using a tostring function with the eval command, sorting results will result in them sorting alphanumerically.

Add another argument that allows the user to choose if they want to convert the currency with the eval or fieldformat command. 

Splunk allows you to validate the argument sent using an eval or boolean expression.

Require that the 'cmd' argument passed to the macro is either fieldformat or eval, if not, send the user an error. Enter a boolean as our validation expression and 

if the boolean is false in the validation error message field and save.

![Screen Shot 2021-07-28 at 9 43 14 PM](https://user-images.githubusercontent.com/15880042/127418491-a5d2e7cf-f3c3-4cd1-9ddb-5b79354f335b.png)

Now when you search, pass a command name as an argument

```JavaScript
index=sales sourcetype=vendor_sales
| stats avg(sale_price) as Average_Price by product_name
| `convertUSD("Average_Price")`
| sort - Average_Price
```



### Expanding Search
------------

Splunk allows you to preview your search by expanding the entire search, without executing it, with it's built-in search expansion tool.

With your search in the search bar use the keyboard shortcut of CTRL + SHIFT+E (linux or windows) OR COMMAND+SHIFT+E (OSX). The search expansion tool will open
and you will be able to see the search as it will be submitted.

![Screen Shot 2021-07-28 at 9 59 56 PM](https://user-images.githubusercontent.com/15880042/127419895-d37f6cb1-24e1-42fd-937c-cada54077d65.png)


