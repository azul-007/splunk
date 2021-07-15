# Filtering and Formatting



[The Eval Command](#the-eval-command)

[Eval Mathematical Functions](#eval-mathematical-functions)

[Eval Convert Values](#eval-convert-values)

[Fieldformat Command](#fieldformat-command)

[Multiple Eval Commands](#multiple-eval-commands)

[Eval Command If Function](#eval-command-if-function)

[Eval Case Function](#eval-case-function)

[Eval with Stats](#eval-with-stats)

[Search Command](#search-command)

[Where Command](#where-command)

[Eval/Where Tips](#eval-//-where-tips)

[Fillnull Command](#fillnull-command)



# Content

### The Eval Command
---------------------

The eval command is used to calculate and manipulate field values: arthmetic, concatenation and boolean operators operators are supported.
Field values created by the eval command are case sensitive. The fields - Bytes command, removes the Bytes field from the column results.

```Javascript
index=network sourcetype=cisco_wsa_squid
| stats sum(sc_bytes) as Bytes by usage
| eval bandwidth = round(Bytes/1024/1024,2)
| fields - Bytes
```


### Eval Mathematical Functions
---------------------
```JavaScript
index=web sourcetype=access_c* product_name=* action=purchase 
| stats sum(price) as total_list_price, sum(sale_price) as total_sale_price by product_name
| eval discount = round(((total_sale_price - total_list_price) / total_list_price)*100)
| sort - dscount 
| eval discount=discount."%"
```



### Eval Convert Values
---------------------

You can convert numerical values to strings with the *tostring* function of the eval command.

```JavaScript
index=web sourcetype=access_c* product_name=* action=purchase 
| stats sum(price) as total_list_price, sum(sale_price) as total_sale_price by product_name
| eval total_list_price="$" tostring(total_list_price,"commas")
```



### Fieldformat Command
---------------------

The fieldformat command allows you to format values without changing characteristics of underlying values.
It has the same functions of the eval command and will allow you to sort on it's fields.

```JavaScript
index=web sourcetype=access_c* product_name=* action=purchase 
| stats sum(price) as total_list_price, sum(sale_price) as total_sale_price by product_name
| eval total_list_price="$" tostring(total_list_price,"commas") 
| fieldformat total_sale_price="$" + tostring(total_list_price,"commas")
```


### Multiple Eval Commands
---------------------




### Eval Command If Function
---------------------

The if function takes three arguments: if (x,y,z)
- The first arg is a boolean expression. If it evaluates to true the second argument will be used.
- If it evaluates to false, the third argument will be used. 
- The second and third arguments must be in quotes if they are not numerical.

```JavaScript
index=sales sourcetype=vendor_sales
| eval SalesTerritory = if (VendorID < 4000, "North America", "Rest of the World")
| stats sum(price) as TotalRevenue by SalesTerritory
```


### Eval Case Function
---------------------

Behaves similar to the if function, except it takes multiple boolean expressions and returns the correspnding
argument that is true.

```JavaScript
index=web sourcetype=access_combined
| eval httpCategory=case(status>=200 AND status<300, "Success", status>=300 AND status<400, "Redirect", status>=400 AND status<500,
"Client Error", status>=500, "Server Error", true(), "Something Weird Happened")
```


### Eval with Stats
---------------------




### Search Command
---------------------

The search command can be used to filter results at any time in the search. It allows you to filter your results further down the search pipeline.

The example below shows a search that finds how many times an employee has visited a prohibited site in the last 30 days.

```JavaScript
index=network sourcetype=cisco_wsa_squid usage=Violation
| stats count(usage) as Vists by cs_username
| search Visits > 1
```




### Where Command
---------------------

Uses the same expressions as eval.
The example below shows a report of employees that have visited more personal sites than business sites over the past 7 days.

```JavaScript
index=network sourcetype=cisco_wsa_squid 
| stats count(eval(usage="Personal")) as Personal, count(eval(usage="Business")) as Business by username
| where Personal > Business | where username!="lsagers" | sort -Personal
```

Without the double quotes around lsagers, Splunk will treat the argument as a field, with it, it'll be treated as a literal.



### Eval/Where Tips
---------------------

- Inside either askerisks cannot be used as a wildercard. Use the like operator with either the %(matches multiple characters) or _ (matches one) characters.
- If you want to determien if a field is null or not, use the isnull or isnotnull functions
- When evaluating a field value, values are case sensitive
- Use double quotes for where clauses



### Fillnull Command
---------------------

If you run a report that includes nulls for some data, your report will display with empty fields.

By default the null values are filled with zeros, but by using a value argument, any string can be used.

```JavaScript
index=sales sourcetype=vendor_sales
| chart sum(price) over product_name by VendorCountry 
| fillnull value="fill with something"
```
