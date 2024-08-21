
## Handling Errors in Data Files

![[40-load-customer-data-file.png]]


![[41-we-can-see-errors.png]]


![[42-select-options-to-handle-errors.png]]



![[43-select-keep-errors-show-error-records.png]]

Open the actual data file to check for the error records. 

![[44-search-error-records.png]]


![[45-identifies-error-records.png]]


![[46-if-needed-we-can-replace-errorvaluess.png]]

Or we can straight away remove error records. 

![[47-remove-error-records-option.png]]


![[48-use-new-source-option-to-load-data.png]]

![[49-load-dimension-data.png]]



![[50-select-more-option.png]]



![[51-use-folder-option.png]]


![[52-browse-for-data-file-folder.png]]


![[53-select-final-fact-data-folder.png]]


![[53-files-inside-folder-is-shown-we-neeed to-combine.png]]

![[54-preview-of-first-file-shown.png]]


Query with the folder name as been created. Along with that some other helper queries had been created. 

![[55-folder-connect-query.png]]

![[56-data-model-view-shows-connection.png]]


![[57-connect-customer-key-of-sales-and-customer-data.png]]

Another Error is encountered

![[58-another-error-in-customer-data.png]]

We can see an empty record is present. This is causing the error in the model. Let's delete this empty record. 

![[59-empty-record.png]]


![[60-remove-empty-record.png]]


![[61-correctly-identified-cardinality.png]]

![[62-sales-customer-tables-connected.png]]


![[63-renaming-sales-data-table.png]]

## Formatting the Data Fields

### Format the Date Fields

![[64-select-date-fields-which-needs-to-be-formatted.png]]


![[65-change-the-display-format.png]]

Let's do the same formatting change to the other date fields in the other data tables like Sales. 

![[66-date-formatted-in-sales-table.png]]

### Formatting Numerical Columns

![[67-select-numerical-columns-which-should-not-be-summarized.png]]

![[68-select-donot-summarize-option.png]]

Even though fields like `ProductPrice ProductCost` has meaning when they are summarized, as a practice we should configured them not be automatically summarized. This is because we write explicit measures for all the calculations and at the measure definition we define what the summarized method is i.e. `SUM or MAX AVERAGE`. 

![[69-format-all-numeric-fields-to-donot-summarize-option.png]]

## Let's see how the PowerBI Model Works

![[70-data-model-connections-direction.png]]

Let's Start with Sales Data Set. When you look at the way we have connected the tables. 

![[71-table-connection-options.png]]

![[72-productkey-in-sales-table.png]]


![[73-more-product-details-present-in-products-table.png]]

Let's see how we can use these different data points together in a single visual like a simple table. 

![[74-both-sales-products-details-in-a-single-table.png]]


![[75-bringing-customer-data-points.png]]

![[75-bringing-customer-data-points.png]]


![[76-adding-customer-data-to-table-visual.png]]
