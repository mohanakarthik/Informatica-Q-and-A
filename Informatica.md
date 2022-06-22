# Informatica Q&A

## Index

[1. Difference between Joiner and Lookup](#1-difference-between-joiner-and-lookup)\
[2. How to check if a field value is date?](#2-how-to-check-if-a-field-value-is-date)\
[3. Difference between union and union all transformation](#3-difference-between-union-and-union-all-transformation)\
[4. Is union transformation active or passive?](#4-is-union-transformation-active-or-passive)\
[5. Is Stored procedure active or passive why?](#5-is-stored-procedure-active-or-passive-why)\
[6. How many conditions can filter transformation have?](#6-how-many-conditions-can-filter-transformation-have)\
[7. Router vs filter transformation which is better?](#7-router-vs-filter-transformation-which-is-better)\
[8. How to update target table if primary key is not defined on target?](#8-how-to-update-target-table-if-primary-key-is-not-defined-on-target)


## 1. Difference between Joiner and Lookup

### Joiner:
> Join tables with multiple joins like inner join, master outer(right join., detail outer (left join.	Only left outer.\
> Override cannot	Override query can be written.\

### Lookup: 
> Only left outer join can be performed.
> No sorting option in lookup

### Advantage: 

> Sorter join on flat files will be more faster in joiner.

## 2. How to check if a field value is date?

> Use ISDATE function in informatica expression. If output is 0 then its a date value(TRUE., if output is 1 then its not a date value(False..

## 3. Difference between union and union all transformation

> **Union all** transformation contains duplicates\
>Union Transformation will not have duplicates

## 4. Is union transformation active or passive?  

> Its active as sequence of rows changes in union.

## 5. Is Stored procedure active or passive why?

> Its passive as it doesnt not change the number of rows passing to target.

## 6. How many conditions can filter transformation have? 

> Unlimited.

## 7. Router vs filter transformation which is better? 

> Router is better as we can put multiple conditions in different groups at one place.
> Incoming dataset has to pass different groups and so we get multiple streams as output from router.\
> "Router" conditions will not block the incoming record , "filter" condition blocks the incoming record on the condition given.

## 8. How to update target table if primary key is not defined on target?

> Use update override,
> Update table
```sql
set sales=TU.sales where emp_name=TU.emp_name and emp_name='Mike Smith';
```
Requirement is to update the table SALES_DATA for the field, sales in target with the incoming data in the field TU.sales based on the emp_name, Mike Smith.

## 9. Can multiple ports can be returned in unconnected lookup transformation?

> Yes, multiple ports can be returned in unconnected lookup transformation through a lookup override.

### Step 1: 
Write the query at lookup override in unconnected lookup, Select first_name||'-'last_name as full_name from table

### Step 2: 
Create port full_name in unconneced lookup and return this column.

### Step 3: 
Segregate the full_name column at expression by creating spearate ports for firstname and lastname

## 10. If sorted input is passed to aggregator after selecting sorted input option at aggregator transformation, what will happen? 
> Session will fail.

## 11. What will be output of not selecting any group by column in aggregator transformation
> Integration service will display last record of dataset.

## 12. How to find where is the performance issue in informatica if a mapping is running slow
>Open session log and search busy percentage and see if we have high busy percentage at source/target or in any other transformation.

## 13. Tell me one limimation where we cannot use the pushdown optimization technique.
> We cannot use this in different databases, sources and target databases has to be in same datatbase for this to get implemented.

## 14. How to delete duplicate records using informatica using tansformation:
1. Distinct option in source qualifier
2. Check distinct option in sorter
3. Use aggregator and do group by on all columns.
4. Using dynamic cache in lookup and it will drop the duplicate record

## 15. Full flow of SCD type 2, proceed with telling how and when which transformation will be used?
1. Lookup transformation : Lookup on target to see if the soruce record exist in target or not.
2. Expression transformation : Create a flag using the return value from step 1(lookup transformation..
3. Router: To flag records as insert/update basis flag generated in step 2(Expression transforamtion..
4. Update strategy(just for updates.: To update the target record based the source record.

## 16. What is dynamic and static cache in lookup tranformation and where its used, is it used in your project?
> Dynamic cache in lookup is used when the cache is updated 1st and then the target in the same pipeline.
> Static cache will not update during mapping run.

> Dynamic cache in lookup is important when we have duplicae record in sources and can be used to drop the duplicates.

## 17. What will be the ouput when we select to "return all values on multiple match" in lookup transformation?
 > Informatica will duplicate the rows in case of multiple match. If one source record is matching with 4 rows in lookup table, then the downstream transformation after lookup will ahve 4 soure records.

## 18. In which column ranking position like 1,2,3 is stored in rank transformation? 
>Rank index column(by default created while creating transformation..Its a output port only, it will store top/bottom 5 or whatever number we specify in this property.

## 19. How to run informatica workflow from unix box or unix command and how to use it? 
>pmcmd command is used to run workflow from unix box or get task details. Example : pmcmd startworkflow -sv Integration service name -d domain -u usernmae -p password -f foldername workflowname

## 23. In which column ranking position like 1,2,3,is stored in rank transformation? 
>What we use update strategy in mapping,w hat configuration at session level is done so that informatica service does what is coded in update strategy transformation ? "Data drivven" option has to be enabled at session level.

## 24. How to get value returned from database in middle of pipeline in informatica designer? 
>Use stored procedure tranformation and call the procedure in transformation and the same will hit the database and get value returned from there which can be used in downstream transformation.

## 25. What is tracing level and how many types of tracing level?

Terse: Logs initialization information, error messages and notification of rejected data in session log file

Normal: Integration service logs initialization and status information erros encountered and skipped rows due to transformation row errors.Summarizes session results but not at the level of individual rows.

Verbose initialization: In addition to normal tracing, the intergration service logs each row that passes into the mapping. Also notes where the Integration truncates string data to fit the precision of a column and provides detailed information statistics. When you configure the tracing level to verbose data, Integration servince writes row data for all rows in block when it processes a tranformation.

## 26. How to reuse lookup cache? 
1. Enable "Lookup cache persistent" in lookup properties and tranformation will read cache in unix box created from another mapping.
2. Give the cache file name in "File name prefix" in lookup properties and same will be read by lookup transformation on mapping run.

## 27. What are audit tables in informatica? 
>Audit tables are created before load starts si tgat we create a etrt ub table that load with this load name has started at this time and ended at this time, these many rows are processed, source read rows and target loaded rows count are also captured in audit tables.

## 28. Difference between mapping parameter and variable?
> Value of mapping parameter will remain constant and fixed during sesion bu mapping variable will chane during or after the session run and final value will be saved to repository and the same value will be used in the next session run.

## 29. Which table is designed a smaster in joiner transforamtion and why? 
>The tables with less rows will be designated as master so that less number of join iterations happens.

## 30. Why lookup transformation is active? 
>It can return multiple rows when it matches with multipe rows in lookup table.

## 31. Which type of cache you have used in your project and why? 
>If I need to drop the duplicates using dynamic cache lookup, how to achieve this? Static cache as we dont had the duplicates in my source system and majority ot is used to capture if source has no change or it is insert or update.

## 32. How many joiners do we need if we are not using the source qualifier to join sources? 
> n-1

## 33. If mapping parameter or variable value is not found in parameter file, where will integration service try to locate it next?
>Values are searched in below sequence,
>Value in parameter file
>Value saved in repository.
>Initial value defined in mapping and parameters under mapping tab.
>Default value.

## 34. What is difference between full and incremental load? 
>Loading full source data is full load. Loading only new records leaving the old ones behind is called as incremental or delta

## 35. How to load incremental data using informatica? 
>Declare a mapping variable in mapping and parameters under mapping tab in designer and use the same in source qualifier query to filter the new records and the value of same can be set during the mapping run and same will be saved to repository to select the new record for next session run.

## 36. Where to use double dollar and single dollar while using mapping/session parameter/variable? 
>Mapping parameters/variable are declared by $$, database connection parameter and target table name/database name are defined with parameter are declared by $ sign.

## 37. What is mapping and which transforamtions cannot be used in it? 
>Mapplet is a set of transformations which are reusable, they are built so that they are built one time and can be used in several mapping where we have the same business requirement and need to use same set of transformations.

>Below transformations cannot be reused,
1. Target
2. Normalizer
3. XML sources
4. Cobol sources.

## 38. If we have 50 paritions on source then how many and what types of threads are created in informatica, also tell us different kinds of threads are created? 
>50 partitions will create 50 threads, there will be 50 reader/writer/transformation threads whcih will run in parallel to load data but remeber we would need to add 50 conditions in session source level so that 50 paritions have distinct records.

## 39. How many types of partioning we have in infromatica and what are they? 
>There are 6 types of partitions but the most used is round robin and passthrough.
    Round Robin: Data is evenly dstributed to all partitions
    Pass through : Data remain same in same parition after passing through passthrough partition.

## 40. Why we use automation tools like CA7, TWS when we have informatica scheduler? 
> We cannot se the dependency in informatica schedular but in external schedular tools we can.

## 41. How informatica will behave when source filter and sql query both are defined in source qualifer transformation?
> Informatica will discard the filter and consider sql query for processing.

## 42. Have you ued normalizer transformation in your project and what it does?

>Normalizer is used to convert a row to column.
>2 columns are generated by default GK and GCID.
>GCID : This will give the number corresponding to no of occurs specified in transformation like 1,2,3.
>GK: This field will have the value of corresponding columns which will display in rows now for that record.

## 43. What kind of performance tuning you have done in your project?
> Write a lookup override query when doing lookup on big table. Use data from stage table to join and select just the records required from target.
>Use buk loading when we dont need to recover session.
>Drop index at target before loads starts and create indexes after target loading.
>Use sorted input before aggregator
>Filter the records which are not required at source qualifier trasnformation itself and not at later state in pipeline.

## 44. What was the complex mapping you made, tell the requirement.
 >Give a scenario from your project where you have used 8-9 lookups some complex transformation like java or sql.

## 45. How to execute databse proedure from informatica?
> Use stored proedure transformation and call the procedure in transformation and the same will hit the database and get value returned from there which can be used in downstream transformation.

## 46. Change Data Capture -

## 47. Tell me a transformation other than normalizer which increases the output row count.
 >Router : As same row can pass multiple groups and hence the output row count is more than input row count in some cases.

## 48. difference between stop and abort in workflow session.
> Stop command tells the integration service to stop reading session data, but will continue writing and commiting data to targets.
> A abort commad works exactly like the stop command, but it will tell the  IS to stop processing and committing data to targets after 60 seconds. If all processes are not complete after this time out period, session gets terminated.

## 49. Where you have used mapping parameters and variables? 
>Parameters are used where we want constant value like source db parameterization, some date parameterization for which value is fixed during mapping run.
>Variable is whose value eep changing during session and final value is saved to repository like mapping variable creation for incremental load.

## 50. Functions used in the project ?
> Decode, IFF, ISNUL, REG_MATCH, REG_REPLACE, ISDATE ..

## 51. Session on grid.
> Running a session on grid, it runs on many nodes(machines. and uses more system hardware as we are running a single session on multipe threads.

## 52. Stop on errors?
> How many erros IS should stop the session, default value of it is 1 which means session stops after 1 error, We can set it to 5 to stop after 5 erros or to -1/0 to never stop. Config tab

## 53. What is line sequential buffer length property at session level in informatica? 
 >It is the maximum length of bytes that IS can read from flat file source, decrease its value in CONFIG TAB to improve performance.

## 54. How you get source data in your project?
>Sources were received from external vendors.


**LEARN MORE ABOUT**
 1. PARITIONING
 2. LOOKUP

 **CHANGE DATA CAPTURE**



