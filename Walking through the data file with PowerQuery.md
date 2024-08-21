## Importing the combined data set into PowerBI 

+  Step 1 - Open PowerBI Desktop and select get data option

![[01-get-data-option.png]] 

+ Step 2 - Select Get Data using Excel workbook
 ![[02-get-data-using-excel.png]]

+ Step 3 - Select Sheet / Table and select "Transform Data" Option

![[03-select-excel-sheet-name-and-transformat-data.png]]

+ Step 4 - Now we are in PowerQuery, go to View Menu and select below options

![[04-enable-data-profiling-options.png]]

+ Step 5 - Change the name of the Query - Sales

![[06-set-query-name-to-sales.png]]

+ Step 6 - Set the profiling based on entire data set and then check for auto detected column data types and for Errors

![[05-check-for-errors-auto-selected-data-type.png]]

+ Step 7 - If we are not happy with auto detected data types we can change. 

Change the Data type of the `OrderDate` column to `Date` instead of `DateTime` 

![[07-change-auto-detected-date-types.png]]
We can directly change the `M Code` as well 

![[08-change-M-code-for-changing-datatypes.png]]


+ Step 08 - Select `Close and Apply`

![[09-close-power-query.png]]


