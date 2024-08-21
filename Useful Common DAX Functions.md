## Math and Stats
Functions used for *aggregations* or iterative, row-level calculations

### SUM
Evaluates the sum of a columns

```DAX
Total Order Quantities = SUM( Sales[OrderQuantity] )
```

### AVERAGE
Returns the average (arithmetic mean) of all the numbers in a column

```DAX
Total Average Sales Amount = AVERAGE( Sales[Transaction Sales Amount] )

Total Average Cost Amount = AVERAGE( Sales[Transaction Cost Amount] )

Total Average Profit Amount = AVERAGE( Sales[Transaction Margin] )
```

### MAX
Returns the largest value in a column or between two scalar expressions 

```DAX
Maximum Product Price = MAX( Products[ProductPrice] )
Maximum Product Cost = MAX( Products[ProductCost] )
```

### MIN
Returns the smallest value in a column or between two scalar expressions. 

```DAX
Min Product Price = MIN( Products[ProductPrice] )
Min Product Cost = MIN( Products[ProductCost] )
```

## DIVIDE
Performs division and returns the alternate result (or blank ) if DIV / 0

```DAX
Total Sales % of Male Customers =

var _male_sales = CALCULATE(
    [Total Sales Amount],
    Customers[Gender] == "Male"
)

var _female_sales = CALCULATE(
    [Total Sales Amount],
    Customers[Gender] == "Female"
)

var _total = _male_sales + _female_sales

RETURN
//_male_sales
//_female_sales
//_total

DIVIDE( _male_sales, _total )
```

### COUNT
Count the number of non-empty cells in a column (excluding boolean values)

```DAX
# of Different Product Color = COUNT( Products[ProductColor] )
# of Different Product Names = COUNT( Products[ProductName] )
```

COUNTROWS
Counts the number of rows in the specified table, or a table defined 

```DAX
# of Different Product Categories = COUNTROWS( 'Product Categories' )
# of Different Product Sub Categories = COUNTROWS( 'Product Subcategories' )
# of Customers = COUNTROWS( Customers )
```

### DISTINCTCOUNT
Counts the number of distinct values in a column

```DAX
# of Different Type of Products which we have Sold = DISTINCTCOUNT( Sales[ProductKey] )
# of Different Territories we have sold products = DISTINCTCOUNT( Sales[TerritoryKey] )
```
## Logical
Functions that use conditional expressions (IF/THEN) statements

### IF
Checks if a given condition is met and returns one value if the condition is TRUE, and another if the condition if FALSE

Lets create a new calculated column in the `Customers` table. The name of the column should be `Customer Priority` 

```DAX
Customer Priority =

IF( Customers[AnnualIncome] > 10000 && Customers[TotalChildren] > 0, "Priority", "Standard")

```

### SWITCH
Evaluates an expression against a list of values and returns one of multiple possible expressions. 

Lets create a new calculated column in the `Customers` table. The name of the column should be `Income Level` and `Education Category`

```DAX
In Come Level =
SWITCH(
    TRUE(),
    Customers[AnnualIncome] >= 150000, "Very High",
    Customers[AnnualIncome] >= 100000, "High",
    Customers[AnnualIncome] >= 50000, "Average",
    "Low"
)

Education Category =
SWITCH(
    TRUE(),
    OR( Customers[EducationLevel] == "High School", Customers[EducationLevel] == "Partial High School"), "High School",
    OR( Customers[EducationLevel] == "Bachelors", Customers[EducationLevel] == "Partial College"), "Undergrad",
    Customers[EducationLevel] == "Graduate Degree", "Graduate"
)
```


## TEXT
Functions used to manipulate text strings or value formats

### LEN
Returns the number of characters in a string

### CONCATENATE
Joins two text strings into one

Let's create a new column under customer with their `Full Name` by concatenating the `First Name, Last Name` Columns

```DAX
Full Name = CONCATENATE(
    CONCATENATE( Customers[FirstName], " " ),
    Customers[LastName]
)
```
### UPPER 
Converts a string to UPPER case

### LOWER
Converts a string to LOWER case

### LEFT
Returns a number of characters from the start of a text string
### RIGHT
Returns a number of characters from the end of a text string
### MID
Return a number of characters from the middle

### SUBSTITUTE
Replaces an instance of existing text with new text in a string

### SEARCH
Returns the position where a specified string or character is found, reading left to right. 

Let's say we have the `ProductSKU` column as shown below. If we want to derive a new column named `SKU Category` using that. Where the `SKU Category` is any number of characters before the first hyphen in the `ProductSKU` column

![[129-breaking-product-SKUs.png]]

```DAX
SKU Category = LEFT( Products[ProductSKU], SEARCH( "-", [ProductSKU] ) -1 )
```

## Table
Functions that create or manipulate tables and output tables vs. Scalar values

## VALUES
When a column name is given it returns a list of unique list of values in that column

```DAX
VALUES('Calendar'[Year])

VALUES( 'Product Categories'[CategoryName] )
```
## Filter 
Functions use to manipulate table and filter contexts

### FILTER
Returns a table that represents a subset of another table or expression 

```DAX
FILTER(
    'Product Categories',
    'Product Categories'[CategoryName] == "Bikes" || 'Product Categories'[CategoryName] == "Clothing"
)

FILTER(
    'Customers',
    Customers[EducationLevel] == "Graduate Degree"  
)
```

### ALL
Returns all rows in a table, or all values in a column, ignoring any filters that have been applied. 

```DAX
Total Sales % based on Product Category =

var _all_stales = CALCULATE(
    [Total Sales Amount],
    ALL('Product Categories')
)

var _sales = [Total Sales Amount]

RETURN
DIVIDE( _sales, _all_stales)


Total Sales % based on Continent =

var _sales = [Total Sales Amount]

var _all_sales = CALCULATE(
    [Total Sales Amount],
    ALL( 'Territory'[Continent] )
)

RETURN
DIVIDE( _sales, _all_sales )
```





## Date and Time
Functions used to manipulate *date & time* value or handle time intelligence calculations

### Today
Returns the current date or exact time

```DAX
Using Today = TODAY()
```

### NOW
Returns the current date or exact time

```DAX
Using NOW = NOW()
```

### DAY / MONTH / YEAR
Returns the day of the month (1-31), month of the year (1-12), or year of a given date

Let us create a new column in `Customers` table to show the `BirthYear` of the customer. 

```DAX
Birth Year = YEAR( Customers[BirthDate] )
```

### HOUR / MINUTE / SECOND
Returns the hour (0-23), minute (0-59), second (0-59) of a given datetime value. 

### WEEKDAY 
Returns a weekday number from 1 (Sunday) to 7 (Saturday)

### WEEKNUM
Returns the Week # of the year

### EOMONTH
Returns the date of the last day of the month, + / - a specified number of months

### DATEDIFF
Returns the difference between two dates, based on a given interval (day, hour, year, etc.)

## Iterator Functions

### SUMX

```DAX
Total Sales Amount SUMX Version = SUMX(
    Sales,
    RELATED( Products[ProductPrice] ) * Sales[OrderQuantity]
)

Total Sales Cost SUMX Version = SUMX(
    Sales,
    RELATED( Products[ProductCost] ) * Sales[OrderQuantity]
)
```

## TIME Intelligence
Time Intelligence patterns are used to calculate common date-based comparisons

### Performance to date

```DAX
Total Sales YTD = CALCULATE(
    [Total Sales Amount],
    DATESYTD( 'Calendar'[Date] )
)

Total Sales MTD = CALCULATE(
    [Total Sales Amount],
    DATESMTD( 'Calendar'[Date] )
)
```

### Previous Period

```DAX
Total Sales Previous Year = CALCULATE(
    [Total Sales Amount],
    DATEADD(  'Calendar'[Date], -1, YEAR)
)

Total Sales Previous Month = CALCULATE(
    [Total Sales Amount],
    DATEADD('Calendar'[Date],  -1, MONTH
    )
)
```

### Running Total

```DAX
Sales 7 Days Running Total = CALCULATE(
    [Total Sales Amount],
    DATESINPERIOD( 'Calendar'[Date], MAX( 'Calendar'[Date] ), -7, DAY)
)
```
## Relationship
Functions used to manage & modify table relationships




