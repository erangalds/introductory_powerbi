## Organizing our DAX Measures

![[111-create-new-table-with-enter-data-option.png]]

![[112-select-home-table-to-new-measures-table.png]]

More rest of the sales measures also into the same __Measures Table  

![[113-setting-a-folder-structure.png]]

Drag an drop the rest of the measures to  the same _Base_Sales_Measures Folder

![[114-move-other--measures-to-same-folder.png]]

![[115-delete-empty-data-columnn.png]]

That changes the icon of the _Measures Table 

![[116-measures-table-icon-changes.png]]


## Measures with Filters

### Sales Measures for specific product categories

Let us look at the different types of `ProductCategories` that we have in our data set. 

![[117-different-product-data-points.png]]

Let's say we want `Total Sales of Bikes` 

Let's create a new measure under the _Measures Table

![[118-create-new-measure-in-measures-table.png]]

Type in the below DAX code into the DAX Measure Editor

```DAX
Total Sales Bikes = CALCULATE(
    [Total Sales Amount],
    'Product Categories'[CategoryName] == "Bikes"
)
```

Let's now visualize and validate. 

![[119-validate-total-sales-bikes.png]]


Let's now create few more similar measures. 

```DAX
Total Sales Accessories = CALCULATE(
    [Total Sales Amount],
    'Product Categories'[CategoryName] == "Accessories"
)

Total Sales Clothing = CALCULATE(
    [Total Sales Amount],
    'Product Categories'[CategoryName] == "Clothing"
)
```

![[120-validate-new-measures.png]]

Move the new measures to a new subfolder under _Measures Table

![[121-move-new-measures-to-another-subfolder-inside-measures-table.png]]


![[122-how-the-filtering-measures-work-1.png]]

![[123-how-the-filtering-measures-work-2.png]]

### Sales Measures for specific Countries and Regions

```DAX
Total Sales for Australia = CALCULATE(
    [Total Sales Amount],
    Territory[Country] == "Australia"
)

Total Sales for Germany = CALCULATE(
    [Total Sales Amount],
    Territory[Country] == "Germany"
)

Total Sales for Europe = CALCULATE(
    [Total Sales Amount],
    Territory[Continent] == "Europe"
)

Total Sales for North America = CALCULATE(
    [Total Sales Amount],
    Territory[Continent] == "North America"
)

```


![[124-validate-measures.png]]

## Multiple Filters in the same DAX Measure

Before writing the DAX query, let us quickly go and get the below columns data values changed as below using `PowerQuery` Replacing option. 

+ Marital Status : M -> Married / S -> Single
+ Gender : M -> Male / F -> Female

![[125-change-data-points.png]]


![[126-values-changed.png]]

Let us now get below shown 4 matrix charts done, before writing the DAX measures. Because those will be used to validate our measures. 

![[127-matrix-visuals-to-validate-DAX-measures.png]]
#### Both Filters from the same data table

```DAX
Total Sales of Male Professional Customerts = CALCULATE(
    [Total Sales Amount],
    Customers[Gender] == "Male",
    Customers[Occupation] == "Professional"
)

Total Sales of Female Clerical Customerts = CALCULATE(
    [Total Sales Amount],
    Customers[Gender] == "Female",
    Customers[Occupation] == "Clerical"
)
```

#### Filters from different data tables

```DAX
Total Sales of Bikes in Europe = CALCULATE(
    [Total Sales Amount],
    Territory[Continent] == "Europe",
    'Product Categories'[CategoryName] == "Bike"
)

Total Sales of Bikes from Male Customers = CALCULATE(
    [Total Sales Amount],
    'Product Categories'[CategoryName] == "Bikes",
    Customers[Gender] == "Male"
)

Total Sales in Europe from Female Customers = CALCULATE(
    [Total Sales Amount],
    Territory[Continent] == "Europe",
    Customers[Gender] == "Female"
)
```

Let's validate the measures 

![[128-validating-measures-with-multiple-filters.png]]

