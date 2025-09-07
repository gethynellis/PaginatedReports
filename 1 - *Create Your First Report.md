## **Create Your First Report**  


---

## Overview  
The estimated time to complete this lab is **20 minutes**.  

In this lab, you will create your first report by using a Wizard.  

The final report will look like the following:

| Sales Order Line Number | English Product Name             | Order Quantity | Unit Price | Sales Amount |
|--------------------------|----------------------------------|----------------|------------|--------------|
| 1                        | Hydration Pack – 70 oz.         | 12             | 31.8942    | 375.0758     |
| 2                        | LL Mountain Pedal               | 6              | 24.2940    | 145.7640     |
| 3                        | Mountain-200 Black, 38          | 13             | 1331.0942  | 16958.1401   |
| 4                        | Long-Sleeve Logo Jersey, XL     | 3              | 29.9940    | 89.9820      |
| 5                        | LL Mountain Frame - Black, 48   | 1              | 149.8740   | 149.8740     |
| …                        | …                                | …              | …          | …            |

---

## Exercise 1: Create your first report  
In this exercise, you will use a Wizard to create your first report.  

The Wizards can be helpful to fast track a report design. Once the Wizard creates a report, it may not look especially good. Often, you will need to refine the report layout. In later labs in this course, you will learn how to style and configure the report layout to meet your precise design requirements.

---

### Task 1: Create the report  

1. Open **Power BI Report Builder**.  
2. In the *Getting Started* pane, select **Table or Matrix Wizard**.  
   - If the *Getting Started* pane doesn’t open, on the **File** ribbon tab, select **Open**.  
3. In the *New Table or Matrix* window, at the *Choose a Dataset* step, click **Next**.  

   *The report doesn’t yet have a dataset—you will create one during a later Wizard step.*  

4. At the *Choose a Connection to a Data Source* step, click **New**.  
5. In the *Data Source Properties* window, in the **Select Connection Type** dropdown, select **Microsoft Azure SQL Database**.  
6. To create the connection string, click **Build**.  
7. Copy the following connection properties from the file:  
   - Server name: `priad.database.windows.net`  
   - Authentication: `SQL Server Authentication`  
   - User name: `readonlyuser`  
   - Password: `Pass@word1`  
8. Check the **Save My Password** checkbox.  
9. In the *Connect To a Database* section, paste the database name: `AdventureWorksDW2021-PRIAD`.  
10. Click **Test Connection**, verify it succeeds, then click **OK**.  
11. In the *Connection Properties* window, click **OK**.  
12. In the *Data Source Properties* window, verify the connection string, then click **OK**.  
13. In the Wizard, click **Next**.  

---

### Task 2: Design the Query  

15. At the *Design a Query* step, expand the **dbo** schema, then expand **Tables**.  
16. Expand **FactResellerSales**, and select the following columns:  
   - `SalesOrderLineNumber`  
   - `OrderQuantity`  
   - `UnitPrice`  
   - `SalesAmount`  
17. Expand **DimProduct**, and select:  
   - `EnglishProductName`  
18. Review the selected fields in the *Selected Fields* pane.  
19. In the *Applied Filters* pane, click **Add Filter**.  
20. Add a filter for `SalesOrderNumber` (FactResellerSales).  
21. Set its value to `SO51721`.  
22. On the toolbar, click **Run Query**.  
23. Review the query result.  
24. In the Wizard, click **Next**.  

---

### Task 3: Arrange Fields  

25. At the *Arrange Fields* step:  
   - Drag `SalesOrderLineNumber` → **Row Groups**.  
   - Drag `EnglishProductName` → **Row Groups**.  
   - Drag `OrderQuantity` → **Values**.  
   - Drag `UnitPrice` → **Values**.  
   - Drag `SalesAmount` → **Values**.  

26. Verify that the layout contains the selected fields.  
27. Click **Next**.  

---

### Task 4: Choose the Layout  

28. At the *Choose the Layout* step, uncheck both options:  
   - Subtotals and grand totals  
   - Expand/collapse groups  

   *The intention is to list sales order line numbers. Subtotals and collapsing groups will be covered in later labs.*  

29. Click **Next**.  
30. At the *Preview* step, review the layout (five columns).  
31. Click **Finish**.  
32. Notice that the Wizard has created a report and added a data region to the canvas.  

---

### Task 5: Preview the Report  

33. To preview, on the **Home** ribbon tab, in the *Views* group, click **Run**.  
34. Review the grid of sales order details.  
35. Close Report Builder (click **X**).  
36. If prompted to save, click **No**.  

---

## Summary  
In this lab, you created your first report by using a Wizard.

 

---
