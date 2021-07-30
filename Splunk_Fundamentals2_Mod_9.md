# Aliases and Calculation Fields

## Table of Contents

Fields alias give you a way to normalize data over multiple sources. You can assign multiple aliases to any extracted field and apply them to lookups.

[Creating a Field Alias](#creating-a-field-alias)

[Calculated Fields](#calculated-fields)


### Creating a Field Alias
------------

- Settings -> Fields -> Add New for the 'Field aliases' type. In the destination app drop down select "search". 
- Create a meaningful name for the field alias.
- Select from sourcetype, source and host. Enter the name of the item to effect.
- Map the existing field on the left, add the name of the alias on the right.
<img width="1044" alt="Screen Shot 2021-07-30 at 7 20 07 PM" src="https://user-images.githubusercontent.com/15880042/127720463-47492652-c325-439c-803b-d813bdcd899b.png">





### Calculated Fields
------------

Calculated fields are best used for repetitive tasks and **must be based on an extracted or discovered field**. Output fields from a lookup table or fields generated from within a search string are not supported.

Create a calculated field by going to Settings:

- Fields..Add New
- In the destination app drop down select "search". 
- Select from sourcetype, source and host. Enter the name of the item to effect.
- Select a name for the field
- Create your eval expression

<img width="1080" alt="Screen Shot 2021-07-30 at 7 21 33 PM" src="https://user-images.githubusercontent.com/15880042/127720528-54264018-ee2a-46f9-83fe-4f2d9ea06016.png">

