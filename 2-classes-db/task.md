# Class Database
Run the following commands:
```
createdb homework
psql -d homework -f setup.sql
```
This will create and populate a database called homework.

It is based on real data from the government found at
https://data.gov.uk/dataset/72eaec8e-0d32-4041-a553-87b852abee64/spend-over-25-000-in-worcestershire-acute-hospitals-psnhs-trust

You can work with it by running
```
psql homework
```
## Submission

Below you will find a set of tasks for you to complete to consolidate and extend your learning from this week. You will find it beneficial to complete the reading tasks before attempting some of these.

To submit this homework write the correct commands after each question.

### 1. Show the date, transaction_no, description and amount for those transactions whose amount is between £30,000 and £31,000.
```sql
"date"	"transaction_no"	"description"	"amount"
"2021-03-01"	37755444	"Flexible endoscope Technical Service"	30238
"2021-03-01"	37632601	"Support and Maintenance for Clinisys Winpath Pathology IT system"	30242
"2021-03-01"	37675451	"Drugs for Spasticity clinics"	30591
"2021-04-01"	37854035	"CALL OFF PO - REMOTE ACCESS"	30000
"2021-04-01"	38014043	"Advisor Projects"	30040
"2021-04-01"	37823809	"CALL OFF ORDER - NETWORKING"	30942
"2021-04-01"	37829728	"Linen services"	30990
```
### 2. Show the date, transaction_no, supplier_inv_no, description and amount for those transactions whose description includes the word 'fee'.
```sql
"date"	"transaction_no"	"description"	"supplier_inv_no"	"amount"
"2021-03-01"	37574010	"Agreement fee as set out in the Report for the Settlement Deed"	"PML0051"	51113
"2021-04-01"	37788824	"Recruitment fee for international nurses"	"I000039418P"	34800
"2021-04-01"	37828209	"DAF - Professional fees"	"11829"	300000
```
### 3. Show the date, transaction_no, supplier_inv_no, description and amount for those transactions whose description includes the word 'Fee'.
```sql

"date"	"transaction_no"	"description"	"supplier_inv_no"	"amount"
"2021-03-01"	37600517	"Overseas Nurses Fees"	"I000038387P"	34800
"2021-03-01"	37750117	"Consultant Fees"	"T034177"	74996
"2021-03-01"	37726776	"Consultant Fees"	"T034397"	461861
"2021-03-01"	37669018	"Consultant Fees"	"T034456"	646944
"2021-03-01"	37788777	"Consultant Fees"	"T034567"	423270
"2021-04-01"	38014054	"Annual Fee"	"42914332"	319646

```
### 4. Show the date, transaction_no, supplier_inv_no, description and amount for those transactions whose description includes the word 'fee' (case insensitive). You will need to search 'https://www.postgresql.org/docs/' to solve this.
```sql
"date"	"transaction_no"	"supplier_inv_no"	"description"	"amount"
"2021-03-01"	37600517	"I000038387P"	"Overseas Nurses Fees"	34800
"2021-03-01"	37574010	"PML0051"	"Agreement fee as set out in the Report for the Settlement Deed"	51113
"2021-03-01"	37750117	"T034177"	"Consultant Fees"	74996
"2021-03-01"	37726776	"T034397"	"Consultant Fees"	461861
"2021-03-01"	37669018	"T034456"	"Consultant Fees"	646944
"2021-03-01"	37788777	"T034567"	"Consultant Fees"	423270
"2021-04-01"	37788824	"I000039418P"	"Recruitment fee for international nurses"	34800
"2021-04-01"	37828209	"11829"	"DAF - Professional fees"	300000
"2021-04-01"	38014054	"42914332"	"Annual Fee"	319646
```
### 5. Show the date, transaction_no, supplier_inv_no, description and amount for those transactions whose amount is £25,000, £30,000, £35,000 or £40,000.
```sql
"date"	"transaction_no"	"supplier_inv_no"	"description"	"amount"
"2021-03-01"	37588987	"11716"	"Waste Volume"	25000
"2021-03-01"	37698700	"11795"	"Waste Volume"	25000
"2021-03-01"	37520209	"INV4131"	"Site surveys and weekly design/Progress Meetings."	25000
"2021-04-01"	37801641	"305719"	"Fire Alarm Infrastructure Replacement"	25000
"2021-04-01"	37854035	"3780119745"	"CALL OFF PO - REMOTE ACCESS"	30000
"2021-04-01"	38059452	"7032500381"	"Recharge of intersystems"	40000
```
### 6. Show the date, the supplier_id, the description and the amount for transactions with the expense area of 'Better Hospital Food'. You could do a query to get the expense_area_id first then do a query to find the dates, supplier_ids and amounts. But it would be better to do this all in one query by linking the tables together using INNER JOINs.
```sql
"date"	"supplier_id"	"description"	"amount"
"2021-03-01"	61	"Meals Volume"	105000
"2021-03-01"	61	"Meals Additional Variations"	32558
"2021-03-01"	61	"Meals Volume"	100000
```
### 7. Show the date, supplier name, description and amount for transactions with the expense area of 'Better Hospital Food'. You will need to INNER JOIN another table to be able to do this.
```sql
"date"	"supplier"	"description"	"amount"
"2021-03-01"	"WORCESTERSHIRE HOSPITAL SPC PLC"	"Meals Volume"	105000
"2021-03-01"	"WORCESTERSHIRE HOSPITAL SPC PLC"	"Meals Additional Variations"	32558
"2021-03-01"	"WORCESTERSHIRE HOSPITAL SPC PLC"	"Meals Volume"	100000
```
### 8. We have just received a late invoice for April! Add a new row to the spends table:

```sql
    dated 1st April 2021
    with a description of 'Computer Hardware Dell'
    transaction number is 38104091 and the supplier's inv no is '3780119655'
    the supplier is 'COMPUTACENTER (UK) LTD' (id 16)
    the expense type is 'Computer Hardware Purch' (id 7)
    the expense area is 'ICT Contingency' (id 18)
    for £32,000.
```
### 9. If you examine the dates in the data, you will see they all are dated either 1st march 2021 or 1st April 2021. So if we group on the the date, there will only be two groups. Show the date and the total amount spent on that date for these two dates by using a GROUP BY clause.
```sql
"date"	"sum"
"2021-03-01"	28674452
"2021-04-01"	22927194
```
### 10. (optional) Great we now know the monthly spend. But it didn't look that good. So I've changed my SELECT query to output this instead:
```
   Month    | Monthly Spend 
------------+---------------
 March 2021 | £ 28,674,452
 April 2021 | £ 22,895,194
(2 rows)
```
Can you work out how to do this?
"to_char"	"sum"
"April     2021"	22927194
"March     2021"	28674452

```sql

```

When you have finished all of the questions - open a pull request with your answers to the `SQL-Coursework-Week1` repository.
