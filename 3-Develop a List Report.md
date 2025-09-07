## Lab Develop a List Report

### Overview
•	The estimated time to complete this lab is 45 minutes.
•	In this lab, you will develop the Salesperson Directory report using the List data region. The report will be based on the AdventureWorksDW2021-PRIAD Azure SQL Database. You will then publish the report to Power BI.
•	The final report will look like the following:

Salesperson Directory example

## Exercise 1: Develop a list report
In this exercise, you will develop a list report.

**Important: There are many repetitive tasks when developing reports. The labs in this course will progressively reduce the detailed step-by-step instructions when detailed steps have already been provided.**

### **Task 1: Create the report**

In this task, you will create the report based on the template created previously. The typical development steps for each report developed in this course will be:

i. Create a report based on a report template, using a friendly report name

ii. Add data source(s) to connect to data store(s)

iii. Add dataset(s) to retrieve query result(s)

iv. Configure report parameters, if required

v. Add an expression to the subtitle text box to reflect the report parameter values

vi. Add and configure report items to the report body

vii. Remove any excess height from the report body

### Step by Step Instructions

The steps for this lab are as follows

1.	Open a new instance of Power BI Report Builder.
2.	In the Getting Started window, click Open.
Power BI Report Builder – Getting Started window (Page 3)

3.	In the Open window, navigate to the <CourseFolder>\PowerBIPRIAD\MySolution folder.
Important: If you didn’t successfully complete Lab 02B, you can open the solution template found in the <CourseFolder>\PowerBIPRIAD\Lab02B\Solution folder.
4.	Select the Portrait template, and then click Open.
5.	On the File ribbon tab, select Save As.
6.	Save the report as Salesperson Directory, to the <CourseFolder>\PowerBIPRIAD\MySolution folder.
Save As dialog with report name "Salesperson Directory" (Page 4)

Tip: It’s a good practice to save the file with the full name of the report. By default, this will become the name of the report in Power BI. Also, the file name will be displayed in the report title text box (as defined in your report template).


### Task 2: Create the data source
In this task, you will create a report data source for the AdventureWorksDW2021-PRIAD Azure SQL Database.
1.	In the Report Data pane (located at the left), right-click the Data Sources folder, and then select Add Data Source.
Add Data Source context menu (Page 5)

2.	In the Data Source Properties window, in the Name box, replace the text with AdventureWorksDW.
Data Source Properties – naming the data source (Page 5)

3.	In the Select Connection Type dropdown list, select Microsoft Azure SQL Database.
4.	To create the connection string, click Build.
5.	Copy the following connection properties from the MyEnvironment.txt file (located in <CourseFolder>\PowerBIPRIAD\MySolution\):
o	Server name: priad.database.windows.net
o	Authentication: SQL Server Authentication
o	User name: readonlyuser
o	Password: Pass@word1
6.	Check the Save my Password checkbox.
7.	In the Connect to a database section, in the Select or enter a database name dropdown list, paste in the database name: AdventureWorksDW2021-PRIAD.
8.	Click Test Connection, and verify that the connection succeeds, then click OK.
Important: If the connection doesn’t succeed, it could be because you’ve entered incorrect connection details, or a firewall doesn’t permit you to connect to the Azure SQL Database. If you suspect it’s the latter case, you could open the firewall port, or try another network (for example, tether to your mobile device). For more information, see Azure SQL Database and Azure SQL Data Warehouse IP firewall rules.
9.	In the Connection Properties window, click OK.
10.	In the Data Source Properties window, in the Connection String box, notice that the connection string has been inserted.
11.	Click OK.
12.	In the Report Data pane, verify that the data source is listed.
13.	Save the report.


### Task 3: Create the dataset
In this task, you will create the main report dataset by using the relational query designer.
1.	In the Report Data pane, right-click the AdventureWorksDW data source, and then select Add Dataset.
2.	In the Dataset Properties window, in the Name box, replace the text with dsMain.
Datasets must be defined with a unique name within the report. The practice used in this course is to name the principal dataset as dsMain. Also, take care to enter the name in the correct case — expression references are always case-sensitive.
3.	To define the dataset query, click Query Designer.
(If prompted, re-enter the same credentials you entered earlier.)
4.	If necessary, maximize the Query Designer window.
5.	In the Query Designer window, in the Database View pane (at the left), expand the dbo schema, and then expand the Tables folder.
6.	Expand the DimEmployee table, and then check the following six columns:
o	FirstName
o	LastName
o	Title
o	EmailAddress
o	Phone
o	EmployeePhoto
7.	Expand the DimSalesTerritory table, and then check the following two columns:
o	SalesTerritoryRegion
o	SalesTerritoryGroup
Query Designer with selected fields (Page 7)

8.	In the Selected Fields pane (at the top-right), review — but do not change — the list of fields.
(All selected columns have become dataset fields.)
9.	Beneath the Selected Fields pane, notice the Relationships section, which by default is collapsed.
10.	At the far right of Relationships, expand the section to reveal the pane (use the double-chevron button).
11.	In the Relationships pane, notice that an inner join relationship was created.
The relationship was created automatically when columns from different tables were selected. The designer will automatically create a relationship when there’s a foreign key in the database. It’s possible to create or remove relationships and modify the join type for existing relationships. In this instance, there’s no need to change the relationship join type.
12.	In the Applied Filters pane (at the bottom-right), click the Add Filter button.
13.	Notice that an item was added to the Applied Filters pane.
14.	Modify the item to filter by the SalesPersonFlag column of the DimEmployee table.
15.	In the corresponding Value box, enter TRUE.
16.	At the bottom-right (above the Cancel button), use the double-chevron to reveal the Query Results pane.
17.	On the toolbar, click Run Query.
Query Designer after adding filter and running query (Page 8)

18.	Review the query result.
19.	To finalize the query design, click OK (at the bottom-right of the Query Designer window).
20.	In the Dataset Properties window, in the Query box, review the T-SQL query statement, noting the FROM clause table joins and the WHERE clause filter.
21.	At the left of the window, select the Fields page.
22.	To add a calculated field, click Add, and then select Calculated Field.
Calculated fields extend the fields collection with fields based on expressions. They can be useful when you need to transform the source data into a single field, and when you don’t have the skills to write the expression in the native query.
23.	Notice the new field is appended to the bottom of the field list.
24.	In the Field Name box, enter Salesperson.
25.	At the left of the Field Source box, click the function (fx) button.
26.	In the Expression window, enter the following expression:

 	=UCase(Fields!LastName.Value) & ", " & Fields!FirstName.Value
 	This expression converts the value of the LastName field to upper case, and then concatenates it to a comma and a space, followed by the value of the FirstName field.
27.	Click OK.
28.	Create a second calculated field named GroupRegion, using the following expression:

 	=Fields!SalesTerritoryGroup.Value & ": " & Fields!SalesTerritoryRegion.Value
 	This expression concatenates the two field values together.
29.	In the Dataset Properties window, click OK.
30.	In the Report Data pane, verify that the dataset is listed.
31.	Save the report.
Task 4: Develop the report layout
In this task, you will add a List to the report body, and lay out the dataset fields using text boxes, an image, and a line. You will also configure the List to sort the data by salesperson.
1.	To add a List, right-click inside the report body, and then select Insert | List.
A List is a rectangular template allowing free-form layout of report objects. (You will learn about the List data region in Module 05.)
2.	Set the size properties of the List:
o	Location, left: 0
o	Location, top: 0
o	Size, width: 7.5
o	Size, height: 1.6
3.	From the Report Data pane, drag the Salesperson field and drop it inside the List.
(Dropping a dataset field into the report designer adds a text box configured to display that field. Since the field was dropped inside the List, the List is automatically bound to the dsMain dataset.)
4.	Right-click the text box, and then select Expression.
5.	Review the simple expression. (It retrieves the Value property of the Salesperson field.)
6.	Click Cancel.
7.	Configure the following properties for that text box:
o	Font size: 18pt
o	Location, left: 1.2
o	Location, top: 0
o	Size, width: 6.3
o	Size, height: 0.3
8.	From the Report Data pane, drag the following four fields into the List, placing each directly beneath the previously added text box:
o	GroupRegion
o	Title
o	Phone
o	EmailAddress
9.	Configure each of the four text boxes as follows:
o	Location, left: 1.2
o	Size, width: 6.3
Unfortunately, it’s not possible to multi-select report objects and then modify their location or size properties (each must be adjusted individually).
10.	Modify the Top property for each of the four text boxes as follows:
o	GroupRegion: 0.3
o	Title: 0.55
o	Phone: 0.8
o	EmailAddress: 1.05
11.	Verify that the List design looks like the following:
List layout with text boxes (Page 13)

12.	To add an image, right-click inside the List, and then select Insert | Image.
13.	In the Image Properties window, in the Select the Image Source dropdown list, select Database.
14.	In the Use this field dropdown list, select the EmployeePhoto field.
15.	In the Use this MIME Type dropdown list, select image/jpeg.
16.	Click OK.
17.	Configure the following properties for the image:
o	Location, left: 0
o	Location, top: 0
o	Size, width: 1
o	Size, height: 1.4
18.	To add a line, right-click inside the List, and then select Insert | Line.
19.	Configure the following properties for the line:
o	Location, left: 1.2
o	Location, top: 1.4
o	EndPoint, horizontal: 7.5
o	EndPoint, vertical: 1.4
20.	Verify that the List design looks like the following:
List layout with image and line (Page 14)

21.	To select the List, right-click inside a blank area of the List, and then select Select | Tablix1.
22.	In the Properties pane, ensure that the List height is 1.6.
23.	To sort the List, in the Properties pane, under the Other category, select SortExpressions, and then click the ellipsis (…).
24.	In the Tablix Properties window, click Add.
25.	In the Sort by dropdown list, select [Salesperson].
26.	Click OK.
27.	To remove the excess body height, hover the cursor over the dotted line between the report body and page footer (at the bottom of the report) to reveal a double-headed arrow, and then drag the line up to the bottom of the List.
28.	Verify that the report body width is still 7.5.
29.	Save the report.
30.	Preview the report, and then switch back to design mode.
Task 5: Publish the report
In this task, you will publish the report to your Power BI workspace, and then edit the data source credentials.
1.	To publish the report, on the Home ribbon tab, in the Share group, click Publish.
Publish report to Power BI (Page 16)

2.	In the Save As – Power BI Service window, on the left, select the workspace you created in Lab 01A.
3.	In the File Name box, enter Salesperson Directory.
4.	Click Publish.
5.	When the report has published, click OK.
Confirmation dialog after publishing report (Page 16)

6.	Switch to the Power BI service web browser session.
7.	Wait until a dialog opens notifying you that credentials are required for the new dataset.
Power BI service dialog requiring credentials (Page 17)

8.	In the dialog window, click Continue.
9.	In the settings for the Salesperson Directory report, expand the Data Source Credentials section.
10.	Click the Edit Credentials link.
11.	In the configuration window, re-enter the user name and password.
(You can copy the credentials from the MyEnvironment.txt file.)
12.	Click Sign In.
13.	To open the report, in the Navigation pane of the Power BI service, click the Salesperson Directory report.
14.	On the menu, click Export, and then select PDF.
15.	When the browser has downloaded the file, open it.
16.	Review the report, which consists of four pages.
17.	Close the PDF document.
18.	Leave Power BI Report Builder open (with the Salesperson Directory report still open).
(You will enhance the report design by adding parameters in Lab 04A.)
## Summary
In this lab, you explored Report Builder and learnt how to add and configure various report objects. You developed the Salesperson Directory report using the List data region (the report was based on the AdventureWorksDW2021-PRIAD Azure SQL Database), and then published the report to Power BI.
Terms of use
