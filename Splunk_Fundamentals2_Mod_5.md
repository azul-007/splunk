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




### Where Command
---------------------





### Eval/Where Tips
---------------------




### Fillnull Command
---------------------
