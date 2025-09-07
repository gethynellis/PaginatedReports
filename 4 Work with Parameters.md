# Lab 04A - Work with Parameters

*(Power BI Paginated Reports in a Day -- September 2021 release)*

## Overview

-   The estimated time to complete this lab is 45 minutes.
-   In this lab, you will enhance the *Salesperson Directory* report
    developed in **Lab 03A** by adding parameters.
-   The cascading parameters will look like the following:\
    Cascading parameters screenshot

## Exercise 1: Work with parameters

In this exercise, you will add and configure report parameters to
explore different usage scenarios.

**Important:** There are many repetitive tasks when developing reports.
The labs in this course will progressively reduce the detailed
step‑by‑step instructions when detailed steps have already been
provided.

### Task 1: Add a query parameter

In this task, you will add a query parameter to the `dsMain` dataset of
the *Salesperson Directory* report.

*If you didn't successfully complete* *Lab 03A* *to create the
Salesperson Directory report, you can open the solution report found in
the* `<CourseFolder>\PowerBIPRIAD\Lab03A\Solution` *folder.*

1.  In Report Builder, verify that the *Salesperson Directory* report is
    open from the previous lab.
2.  In the **Report Data** pane, right‑click the **dsMain** dataset, and
    then select **Dataset Properties**.
3.  In the **Dataset Properties** window, click **Query Designer**.
4.  In the **Query Designer** window, in the **Applied Filters** pane,
    add a new filter for the **EmployeeKey** column.
5.  For the **EmployeeKey** filter, check the **Parameter** checkbox.
6.  Click **OK**.
7.  In the **Dataset Properties** window, in the **Query** box, scroll
    down to reveal the parameterised `WHERE` clause.

*For SQL Server database products, query parameters are prefixed with
the at symbol (*`@`*). At query execution time, a parameter value will
be substituted into the query parameter.*

1.  Click **OK**.

2.  In the **Report Data** pane, expand the **Parameters** folder.

3.  Notice the **EmployeeKey** report parameter.

-   Report data showing EmployeeKey parameter

    *Each query parameter added to a query creates a report parameter.
    Commonly, report parameters are used to prompt the report user for
    values, and these values are then mapped to the dataset query
    parameters.*

4.  In the **Parameters** pane (located above the report designer),
    notice the **Employee Key** report parameter.

5.  In the **Report Data** pane, right‑click the **EmployeeKey** report
    parameter, and then select **Parameter Properties**.

6.  In the **Report Parameter Properties** window, in the *Prompt* box,
    replace the text with **Salesperson**.

-   Changing prompt to Salesperson

7.  Click **OK**.

8.  In the **Parameters** pane, notice that the report parameter prompt
    has updated.

9.  Open the **dsMain** dataset properties, and then select the
    **Parameters** page.

10. Notice the mapping of query parameter to report parameter.

-   *The at symbol (*`@`*) used in the shorthand expression denotes that
    the item is a report parameter.*

11. Open the **Expression** window for the *Parameter Value*, and then
    review the expression.

-   *The expression returns the value of the* *EmployeeKey* *report
    parameter. So, effectively the dataset query parameter receives the
    report parameter value entered by the report user.*

12. Close the **Expression** window, and the **Dataset Properties**
    window.

13. In the page header, right‑click the **Subtitle** textbox, and then
    select **Expression**.

14. In the **Expression** window, in the *Category* list, select
    **Parameters**.

15. In the *Values* list, double‑click the **EmployeeKey** report
    parameter.

16. Click **OK**.

17. Preview the report (click **Run** on the **Home** ribbon tab).

18. In the **Salesperson** parameter box, enter `272`.

19. Click **View Report** (located at the right of the parameter area).

-   View Report button highlighted

20. Review the rendered report, for the single salesperson named
    *Stephen Jiang*.

It's likely improbable that a report user would know the employee key
values required to filter the report. In the next task, you will
configure the report parameter to present a dropdown list of salespeople
and configure the report subtitle to display the salesperson's name.

### Task 2: Configure available values

In this task, you will add a dataset to retrieve a list of salespeople,
and then configure the **EmployeeKey** report parameter to present
available values based on the dataset.

1.  Switch to the report designer.
2.  In the **Report Data** pane, right‑click the **AdventureWorksDW**
    data source, and then select **Add Dataset**.
3.  In the **Dataset Properties** window, in the *Name* box, replace the
    text with `dsSalesperson`.
4.  To retrieve a prepared query, click **Import**.
5.  In the **Import Query** window, navigate to the
    `<CourseFolder>\PowerBIPRIAD\Lab04A\Assets` folder.
6.  Select the **dsSalesperson_1.sql** file, and then click **Open**.
7.  In the **Query** box, review the query statement.

*The query retrieves all salespeople and returns two columns: the*
*EmployeeKey* *column, and the full name of the salesperson. The query
result is sorted in ascending order of the salesperson name.*

1.  Click **OK**.

2.  Open the **EmployeeKey** report parameter properties, and then
    select the **Available Values** page.

3.  Set the following available value properties:

    -   **Option:** Get values from a query
    -   **Dataset:** `dsSalesperson`
    -   **Value field:** `EmployeeKey`
    -   **Label field:** `SalespersonName`

-   Available values settings

    *The* *Value* *field is typically assigned a database key value,
    while the* *Label* *field is assigned a user‑friendly text value.
    It's possible to use the same field for the Value and Label fields.*

4.  Click **OK**.

5.  Modify the expression for the **Subtitle** text box, using the
    following expression:

-   =Parameters!EmployeeKey.Label

6.  Preview the report.

7.  In the **Salesperson** parameter dropdown list, select
    **ABBAS, Syed**, and then click **View Report**.

8.  Review the rendered report, and notice the improved page header
    subtitle text.

*If a report defines report parameters, it can't be run until all values
have been entered. To simplify interacting with the report---or to
ensure the report runs immediately upon request---default values can be
assigned to report parameters.*

### Task 3: Configure default values

In this task, you will configure a default value for **EmployeeKey**
report parameter.

1.  Switch to the report designer.

2.  Open the **EmployeeKey** report parameter properties, and then
    select the **Default Values** page.

3.  Set the following default value properties:

    -   **Option:** Get values from a query
    -   **Dataset:** `dsSalesperson`
    -   **Value field:** `EmployeeKey`

-   *Default values can be based on specified values---either constants
    or expressions---or by dataset query results. When multiple rows are
    returned by a dataset and the report parameter is not configured to
    allow multiple values, the first row of the query result is used as
    the default value.*

4.  Click **OK**.

5.  Preview the report.

6.  Notice that the **Salesperson** parameter has been set, and that the
    report ran automatically.

The report now displays only a single salesperson. The enhancements you
will make in the next task will allow report users to select all
salespeople or just a single salesperson.

### Task 4: Configure an All item

In this task, you will modify the report datasets to allow selecting all
salespeople.

1.  Switch to the report designer.
2.  Open the **dsSalesperson** dataset properties, and then click
    **Import**.
3.  In the **Import Query** window, select the **dsSalesperson_2.sql**
    file, and then click **Open**.
4.  In the **Query** box, review the query statement that has been
    modified to become a union query.

*The first* `SELECT` *statement retrieves an "artificial" row that has
an* *EmployeeKey* *value of --1, and a caption within parentheses. It
returns a key value that doesn't exist in the database. It also defines
a label that will appear first when the rows are sorted by the label
values. The first* `SELECT` *statement is merged with the second, which
is the original statement.*

1.  Click **OK**.
2.  Open the **dsMain** dataset, and import the **dsMain_1.sql** file.
3.  In the **Query** box, review the query statement that has a modified
    `WHERE` clause.

*The* `WHERE` *clause returns a single employee, or all employees when
the* `@EmployeeKey` *parameter value is --1.*

*This query may not be very efficient as it likely forces a table scan.
For large tables, you should avoid this type of predicate by defining
the query statement in a stored procedure. The stored procedure logic
could branch to different query statements based on the* `@EmployeeKey`
*parameter value.*

1.  Click **OK**.

2.  Preview the report.

3.  Notice that the **Salesperson** parameter now defaults to
    *(All Salespeople)*, and that all salespeople are retrieved.

-   *The report parameter continues to default to the first row of the*
    `dsSalesperson` *query, which is now the* (All Salespeople) *row.*

4.  Modify the **Salesperson** report parameter to **ABBAS, Syed**, and
    then click **View Report**.

*When available value lists grow to large sizes, they become impractical
and inefficient to present as a single list. To reduce the list size,
it's possible to introduce additional parameters that use a cascading
behaviour to filter other parameter values.*

### Task 5: Configure cascading parameters

In this task, you will introduce a report parameter to filter the
**EmployeeKey** report parameter available values by a sales territory
group selected by the report user.

1.  Switch to the report designer.
2.  Open the **dsSalesperson** dataset properties, and then click
    **Import**.
3.  In the **Import Query** window, select the **dsSalesperson_3.sql**
    file, and then click **Open**.
4.  In the **Query** box, review the query statement and notice the
    `@SalesTerritoryGroup` query parameter added to the third last line.

*The addition of the query parameter requires the sales territory group
value be passed to the query.*

1.  Click **OK**.

2.  In the **Report Data** pane, notice the addition of the
    **SalesTerritoryGroup** report parameter.

-   Report Data showing SalesTerritoryGroup parameter

3.  To create a new dataset, right‑click the **AdventureWorksDW** data
    source, and then select **Add Dataset**.

4.  In the **Dataset Properties** window, in the *Name* box, replace the
    text with `dsSalesTerritoryGroup`.

5.  To retrieve a prepared query, click **Import**.

6.  In the **Import Query** window, select the
    **dsSalesTerritoryGroup.sql** file, and then click **Open**.

7.  In the **Query** box, review the query statement.

-   *The query retrieves the distinct sales territory group values.*

8.  Click **OK**.

9.  Configure the **SalesTerritoryGroup** report parameter to prompt the
    report user for *Group*.

-   SalesTerritoryGroup parameter properties

10. Set the following available values properties:

    -   Use the **Get Values From a Query** option
    -   Set the **Dataset** to `dsSalesTerritoryGroup`
    -   Set the **Value Field** to `SalesTerritoryGroup`
    -   Set the **Label Field** to `SalesTerritoryGroup`

11. Click **OK**.

12. Modify the **dsMain** dataset query by importing the
    **dsMain_2.sql** file.

-   *The* `WHERE` *clause also filters the query result using the*
    `@SalesTerritoryGroup` *parameter.*

13. Modify the report subtitle text box to use the following expression:

-   =Parameters!SalesTerritoryGroup.Value & Iif(Parameters!EmployeeKey.Value = -1, "", " - " & Parameters!EmployeeKey.Label)

    *The expression returns the sales territory group, and then appends
    the selected salesperson when the "all salespeople" item isn't
    selected.*

14. Preview the report.

15. Notice that the **Salesperson** report parameter is disabled.

-   *The Salesperson report parameter available values cannot be
    retrieved until a* *Group* *report parameter value is selected.*

16. In the **Group** parameter dropdown list, select **North America**.

17. In the **Salesperson** parameter dropdown list, notice that ten
    salespeople are listed.

18. In the **Group** parameter dropdown list, select **Europe**.

19. In the **Salesperson** parameter dropdown list, notice that three
    salespeople are listed.

20. Click **View Report**.

21. Review the rendered report.

The final enhancement made to the report parameters will be to enable
the multi‑selection of parameter values.

### Task 6: Configure multi‑value parameters

In this task, you will enable multi‑value selection for the
**EmployeeKey** report parameter.

1.  Switch to the report designer.

2.  Open the **EmployeeKey** report parameter properties, and then check
    **Allow Multiple Values**.

-   Allow multiple values checkbox

3.  Click **OK**.

4.  Preview the report.

5.  In the **Group** parameter dropdown list, select **North America**.

6.  In the **Salesperson** parameter dropdown list, notice that a
    multi‑select parameter will automatically include a **(Select All)**
    item.

*All parameter values are selected because the default values are based
on all rows of the* `dsSalesperson` *dataset.*

*Don't view the report because it will generate an error. You will
return to the report designer to continue configuring the parameters.*

1.  Switch to the report designer.
2.  Modify the **dsSalesperson** dataset properties by importing the
    **dsSalesperson_4.sql** file.

*The query statement no longer includes the "artificial"
(All Salespeople) row.*

1.  Modify the **dsMain** dataset query by importing the
    **dsMain_3.sql** file.

*The* `WHERE` *clause now filters by the* *EmployeeKey* *column using
the* *IN* *operator. The IN operator allows passing a comma‑delimited
list of values, and Power BI will pass multiple employee key values as a
string of comma‑separated values.*

    ![IN operator highlighted](page14-screenshot1.png)

1.  Modify the report subtitle text box to use the following expression:

-   =Parameters!SalesTerritoryGroup.Value & Iif(Parameters!EmployeeKey.Count = CountRows("dsSalesperson"), "", " - " & Join(Parameters!EmployeeKey.Label, ", "))

    *The expression also uses the* `Join` *function to produce a single
    string of selected values, this time using the* *Label* *property of
    the report parameter, and a delimiter value which includes a space.
    The conditional logic tests the count of selected values, and if it
    matches the count of rows in the* `dsSalesperson` *dataset, it
    doesn't output the delimited list.*

2.  Preview the report.

3.  In the **Group** parameter dropdown list, select **Europe**.

4.  In the **Salesperson** parameter, notice all items are selected---do
    not select an item.

5.  Click **View Report**.

6.  Notice that the page header subtitle simply displays the sales
    territory group name.

7.  In the **Salesperson** parameter dropdown list, de‑select one
    salesperson.

8.  Click **View Report**.

*Notice that the page header subtitle displays the sales territory group
name, and a comma‑separated list of the selected salespeople.*

### Task 7: Publish the report

In this task, you will publish the report to your Power BI workspace.

1.  Switch to the report designer.
2.  Publish the report to your workspace, overwriting the
    previously‑published report.
3.  Close Power BI Report Builder.

*The development of the* *Salesperson Directory* *report is now
complete.*

## Summary

In this lab, you enhanced the *Salesperson Directory* report developed
in **Lab 03A** by adding parameters.

