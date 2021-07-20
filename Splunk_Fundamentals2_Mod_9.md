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




### Calculated Fields
------------

Calculated fields are best used for repetitive tasks and **must be based on an extracted or discovered field**. Output fields from a lookup table or fields generated from within a search string are not supported.

Create a calculated field by going to Settings:

- Fields..Add New
- In the destination app drop down select "search". 
- Select from sourcetype, source and host. Enter the name of the item to effect.
- Select a name for the field
- Create your eval expression
