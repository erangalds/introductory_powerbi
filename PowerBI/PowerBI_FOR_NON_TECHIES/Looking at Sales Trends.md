
![[96-looking-at-existing-date-fields.png]]

![[97-sales-cost-profit-based-on-orderdate.png]]

## Concept of using a separate Calendar Table in the model

![[98-create-new-virtual-table-option.png]]

![[99-define-new-table.png]]

![[100-using-calendar-dax-function.png]]

![[101-defined-basic-calender.png]]


![[102-check-newly-created-table.png]]

![[103-new-column-year.png]]

Similarly create few other new columns using below DAX measures. 

+ Column Month : `Month = MONTH( [Date] )`
+ Column Month Name : `Month Name = FORMAT( [Date], "MMMM" )`
+ Column Month Short Name : `Month Short Name = FORMAT( [Date], "MMM" )`
+ Column Year Month Short Name = `Year Month = 'Calendar'[Year] & " " & 'Calendar'[Month Short Name]`
+ Column Year Month Int = `Year Month Int = 'Calendar'[Year]*100 + 'Calendar'[Month]`
+ Column Quarter = `Quarter = QUARTER( [Date] )`
+ Column Quarter Text = `Quarter Text = "Q" & 'Calendar'[Quarter]`
+ Column Year Quarter = `Year Quarter = 'Calendar'[Year] & " " & 'Calendar'[Quarter Text]`
+ Column Year Quarter Int = `Year Quarter Int = 'Calendar'[Year] * 100 + 'Calendar'[Quarter]`


Sorting the Calendar Columns. 

![[104-sorting-calendar-columns.png]]

Sort the columns as below. 
+ Month Name -> Month
+ Month Name Short -> Month
+ Year Month -> Year Month Int
+ Quarter Text -> Quarter
+ Year Quarter -> Year Quarter Int

![[105-connect-calendar-table-with-sales.png]]

![[106-connection-options.png]]

![[107-duplicate-report-tab.png]]

![[108-year-wise-sales.png]]

![[109-year-month-sale-cost-profit.png]]


![[110-adding-average-max-lines.png]]


