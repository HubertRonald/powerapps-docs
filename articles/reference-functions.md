<properties
   pageTitle="Build an expression"
   description="In KratosApps, you can use the operators and functions that this topic describes."
   services="na"
   documentationCenter="na"
   authors="AFTOwen"
   manager=""
   editor=""
   tags=""/>
<tags
   ms.service="kratosapps"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="07/01/2015"
   ms.author="anneta"/>

#Build an expression in KratosApps

As you develop an app, specify its appearance and behavior by building expressions that include the operators and functions in this topic.

**Note** All references to data in the following examples are hypothetical. No data samples accompany this reference.

##Operators

|Symbol|Operator type|Syntax|Description|
|---|---|---|---|
|( )|Parentheses|Filter(T, A &lt; 10)<br><br>(1 + 2) * 3|Precedence-order enforcement, and grouping of sub-expressions in a larger expression|
|+|Arithmetic operators|1 + 2|Addition|
|-||2 - 1|Subtraction and sign|
|\*||2 * 3|Multiplication|
|/||2 / 3|Division|
|^||2 ^ 3|Exponentiation|
|%||20%|Percentage (equivalent to &quot;* 1/100&quot;)|
|=|Comparison operators|Price = 100|Equal to|
|&gt; ||Price &gt; 100|Greater than|
|&gt;=||Price &gt;= 100|Greater than or equal to|
|&lt; ||Price &lt; 100|Less than|
|&lt;=||Price &lt;= 100|Less than or equal to|
|&lt;&gt; ||Price &lt;&gt; 100|Not equal to|
|&amp;|String concatenation operator|&quot;hello&quot; &amp; &quot; &quot; &amp; &quot;world&quot;|Makes multiple strings appear continuous|
|&amp;&amp;|Logical operators|Price &lt; 100 &amp;&amp; slider!value = 20|Logical conjunction|
|&#124;&#124;||Price &lt; 100 &#124;&#124; slider!value = 20|Logical disjunction|
|!||!(Price &lt; 100)|Logical negation|
|exactin|Membership operators|gallery!Selected exactin SavedItems|Belonging to a collection or table|
|exactin||&quot;Windows&quot; exactin “To display windows in the Windows operating system...”|Substring test (case-sensitive)|
|in||gallery!Selected in SavedItems|Belonging to a collection or table<br><br>|
|in||&quot;The&quot; in &quot;The keyboard and the monitor...&quot;|Substring test (case-insensitive)|
|@|Disambiguation operator|MyTable[@fieldname]|Field disambiguation|
|||[@MyTable]|Global disambiguation|
|;|Expression chaining|Collect(T, A); Navigate(S1, &quot;&quot;)|Separate invocations of functions in behavior properties|

### <a name="in_and_exactin_operators"></a>in and exactin operators
You can use the **in** and **exactin** operators to find a string in a data source, such as a collection or an imported table. The **in** operator identifies matches regardless of case, and the **exactin** operator identifies matches only if they're capitalized the same way. Here's an example:

1.  [Show data in a gallery](show-images-text-gallery-sort-filter.md).

2.  Set the **Items** property of the gallery to this function:

    **Filter(Inventory, "E" in ProductName)**

    The gallery shows all products except Callisto because the name of that product is the only one that doesn't contain the letter you specified.

3.  Change the **Items** property of the gallery to this function:

    **Filter(Inventory, "E" exactin ProductName)**

    The gallery shows only Europa because only its name contains the letter you specified in the case that you specified.

### <a name="thisitem_operator_for_galleries"></a>ThisItem operator for galleries
When you [show data in a gallery](show-images-text-gallery-sort-filter.md), you use the **ThisItem** operator to specify which type of data each control in the gallery shows. For example, you can use that operator to specify that an image control shows the design of a product in a catalog, a label shows the name of the same product, and another label shows its price.

For nested galleries, **ThisItem** refers to the innermost gallery's items. Assuming the row fields in the inner and outer galleries don't conflict, you can also use the unqualified field (column) names directly. This approach enables rules in an inner gallery to refer to an outer gallery's items.

##Functions

KratosApps supports the following functions. If you use functions in Excel, you may recognize many of them.

**Note** In the syntax sections of this topic, italics indicate generic text that you replace with values that are specific for your app, and square brackets enclose optional arguments. If a comma appears before an optional argument, you must include the comma if you want to use the argument that follows it.

### <a name="functions_by_category"></a>Functions by category
**Boolean** -- [And](#and), [If](#if), [IsBlank](#isblank), [IsEmpty](#isempty), [Not](#not), [Or](#or)

**Collections** -- [Clear](#clear), [Collect](#collect), [LoadData](#loaddata), [Remove](#remove), [RemoveIf](#removeif), [SaveData](#savedata)

**Date and Time** -- [Date](#date), [DateAdd](#dateadd), [DateDiff](#datediff), [DateTimeValue](#datetimevalue), [DateValue](#datevalue), [Day](#day), [Hour](#hour), [Minute](#minute), [Month](#month), [Now](#now), [Second](#second), [Time](#time), [TimeValue](#timevalue), [Today](#today), [Year](#year)

[More examples](show-text-dates-times.md) of how to manage dates and times.

**Math** -- [Abs](#abs), [Average](#average), [Max](#max), [Min](#min), [Rand](#rand), [Round](#round), [RoundDown](#rounddown), [RoundUp](#roundup), [Sqrt](#sqrt), [StdevP](#stdevp), [Sum](#sum), [VarP](#varp)

**Other** -- [ColorFade](#colorfade), [ColorValue](#colorvalue), [Disable](#disable), [Enable](#enable), [Launch](#launch), [Language](#language), [Navigate](#navigate), [Refresh](#refresh), [RGBA](#rgba), [UpdateContext](#updatecontext)

**Strings** -- [Char](#char), [Concat](#concat), [Concatenate](#concatenate), [EncodeUrl](#encodeurl), [Find](#find), [HashTags](#hashtags), [Len](#len), [Left](#left), [Lower](#lower), [PlainText](#plaintext), [Proper](#proper), [Right](#right), [Substitute](#substitute), [Text](#text), [Trim](#trim), [Upper](#upper), [Value](#value)

**Table** -- [AddColumns](#addcolumns), [Count](#count), [CountA](#counta), [CountIf](#countif), [CountRows](#countrows), [Distinct](#distinct), [DropColumns](#dropcolumns), [Filter](#filter), [First](#first), [FirstN](#firstn), [Last](#last),[LastN](#lastn), [LookUp](#lookup), [RenameColumns](#renamecolumns), [Replace](#replace), [Sort](#sort), [Shuffle](#shuffle), [ShowColumns](#showcolumns), [Table](#table), [Update](#update), [UpdateIf](#updateif)

### <a name="abs"></a>Abs
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Abs**(*Number*)<br>**Abs**(*ColumnExpression*)|
|Description|Returns the absolute value of a number—that is, the number without its sign.<ul><li>**Abs**(<em>Number</em>) returns the absolute value of a number.</li><li>**Abs**(<em>ColumnExpression</em>), given a one-column table of numeric values, returns a one-column table of their corresponding absolute values.</li></ul>|
|Examples|**Abs(-55)** returns 55.<br><br>If a table contained a column named Trend, you could use **Abs(Trend)** in a Result column to return the absolute value of each number in the Trend column.<br/><br/>![Abs function to calculate absolute values](./media/reference-functions/abs.jpg)|

### <a name="addcolumns"></a>AddColumns
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**AddColumns**(*TableName*, *ColumnName1*, *Subexpression1*[, *ColumnName2*, *Subexpression2*, ...])|
|Description|Returns a table that has one or more added columns that contain results of the specified expressions evaluated over the rows in the original input table.|
|Examples|If you had a Sales table that contained a CostPerUnit column and a UnitsSold column, you could create a second table that contained both of those columns plus a third column, named TotalSales, that showed the results of multiplying the values in the first two columns.<br><br>**AddColumns(Sales, &quot;TotalSales&quot;, CostPerUnit \* UnitsSold)**<br/><br/>![AddColumns puts calculated results in new column](./media/reference-functions/add-columns.jpg)<br/>**Note:** This function doesn't modify the original table.</p></blockquote>If you had an Employees table that contained a FirstName column and a LastName column, you could create a second table that contained both of those columns plus a third column, named FullName, that showed the results of concatenating the strings in the first two columns.<br><br>**AddColumns(Employees, &quot;FullName&quot;, FirstName &amp; &quot; &quot; &amp; LastName)**|

### <a name="and"></a>And
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**And**(*Subexpression1*[, *Subexpression2*, ...])|
|Description|Determines whether one or more Boolean values or sub-expressions are all true. (Accomplishes the same outcome as the inline &amp;&amp; operator.)|
|Examples|This expression determines whether a slider's value falls between 50 and 100:<br/><br/> **And(Slider1!Value &gt; 50, Slider1!Value &lt; 100)**<br><br>If a table contained a Dept column and a Salary column, you could use this function in a Result column to show true in all rows in which the value in the Dept column was HR and the value in the Salary column was larger than 200000.<br><br>**And(Dept = &quot;HR&quot;, Salary &gt; 200000)**<br><br>![And returns true if all conditions are true](./media/reference-functions/and.jpg)<br><br>These expressions use the &amp;&amp; operator but return the same results as the previous examples:<br><br>**Slider1!Value &gt; 50 &amp;&amp; Slider1!Value &lt; 100**<br><br>**Dept = HR &amp;&amp; Salary &gt; 200000**|

### <a name="average"></a>Average
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Average**(*Table*, *Subexpression*)<br><br>**Average**(*Subexpression1*[, *Subexpression2*, …])|
|Description|Returns the average (arithmetic mean) of its arguments. You can use this function in these contexts:<ul><li>In a table, this function returns the average of the numbers that the specified subexpression evaluates to.</li><li>When provided scalar numeric inputs—or subexpressions that evaluate to scalar numeric values—this function returns their average.</li></ul>|
|Examples|If you had a Sales table that contained a CostPerUnit column and a UnitsSold column, this expression would compute the average sales:<br><br>**Average(Sales, CostPerUnit * UnitsSold)**<br><br>If you had three sliders, this expression would compute the average of their values:<br><br>**Average(Slider1!Value, Slider2!Value, Slider3!Value)**|

### <a name="char"></a>Char
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Char**(*Number*)|
|Description|Returns the appropriate ASCII character for your platform, based on the value that you supply.|
|Example|**Char(65)**returns:<br><br>A<br><br>**Char(105)** returns:<br><br>i<br><br>**Char(35)** returns:<br><br>#|

### <a name="clear"></a>Clear
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Clear**(*Collection*)|
|Description|Clears all of the items from a collection and returns an empty collection.<br><br>**Important** This function modifies the underlying collection.|
|Example|<ol><li>Create or import a collection named **Inventory**, as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a button, and then set its **OnSelect** property to this function:<br><br>**Clear(Inventory)**</li><li>Press F5, click the **Clear** button, and then press Esc to return to the design screen.</li></ol>To confirm that your collection is empty, press Alt-D, and then click **Collections** in the left navigation bar.|

### <a name="collect"></a>Collect
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Collect**(*CollectionName*, *Item1*[, *Item2*,...])|
|Description|Adds a table, a column within a table, or at least one item to a collection. If the specified collection doesn't exist, this function creates it and adds the item.<br><br>**Important** This function modifies the underlying collection.|
|Examples|To create a collection that contains a column of values that you specify:<br/><br/><ol><li>Add a button, and set its **OnSelect** property to this function:<br><br>**Collect(Products, &quot;Europa&quot;, &quot;Ganymede&quot;, &quot;Callisto&quot;)**<br><br>This function creates a collection that's named **Products** and that contains a row for each of three product names.</li><li>Press F5, click the button, and then press Esc to return to the design workspace.</li><li>(optional) To display a preview of the collection that you created, press Alt-D, and then click **Collections** in the left navigation bar.</li></ol>[Create and update a collection](create-update-collection.md) for more examples.|

### <a name="colorfade"></a>ColorFade
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**ColorFade**(*Color*, *FadeDelta*)|
|Description|Returns a faded or darker version of a color based on a value between -1 and 1, inclusive.|
|Examples|If you add a shape and set its **Fill** property to **Blue** or **Color!Blue**, the shape is a medium blue. If you set that property to **ColorFade(Color!Blue, .5)** or **ColorFade(Color!Blue, -.5)**, the shape is a lighter or darker (respectively) version of the same color.|

### <a name="colorvalue"></a>ColorValue
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**ColorValue**(*ColorText*)|
|Description|Returns the color value that corresponds to a CSS (cascading style sheet) color string.|
|Examples|**ColorValue(&quot;Blue&quot;)**<br><br>**ColorValue(&quot;Fuschia&quot;)**|

### <a name="concat"></a>Concat
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Concat**(*CollectionName*, *Expression*)|
|Description|Concatenates all strings in a column that you specify in a data source that you specify. You can concatenate data in a collection or imported from, for example, Excel or a SharePoint list.|
|Examples|<ol><li>Add a button, and set its **OnSelect** property to this function:<br><br>**Collect(Products, {String:&quot;Violin&quot;, Wind:&quot;Trombone&quot;, Percussion:&quot;Bongos&quot;}, {String:&quot;Cello&quot;, Wind:&quot;Trumpet&quot;, Percussion:&quot;Tambourine&quot;})**</li><li>Press F5, click the button, and then press Esc to return to the design workspace.</li><li>Add a label, and set its **Text** property to this function:<br><br>**Concat(Products, String &amp; &quot; &quot;)**<br><br>The label shows **Violin Cello**.</li></ol>|

### <a name="concatenate"></a>Concatenate
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Concatenate**(*Text1*[, *Text2*, ...])<br><br>**Concatenate**(*ColumnExpression1*[, *ColumnExpression2*, ...])|
|Description|Joins several text strings into one string, or concatenates the output of several expressions that return text but appear in different columns in a table, and returns the concatenated text in its own column.|
|Examples|If you created an input-text control named AuthorName, the following function would prepend &quot;By&quot; to text that the user typed in that control:<br><br>**Concatenate(&quot;By &quot;, AuthorName!Text)**<br><br>If you had an Employees table that contained a FirstName column and a LastName column, the following function would concatenate the data in each row of those columns.<br><br>**Concatenate(Employees!FirstName, &quot; &quot;, Employees!LastName)**<br/><br/>

### <a name="count"></a>Count
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Count**(*Column*)|
|Description|Counts the cells in a table column that contains only numbers.|
|Example|<ol><li>Import or create a collection named **Inventory**, as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**Count(Inventory!UnitsInStock)**<br><br>The label shows **5**, the number of cells that are in the **UnitsInStock** column and that contain numbers.</li></ol>|

### <a name="counta"></a>CountA
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**CountA**(*Column*)|
|Description|Counts the cells that aren't empty in a table column. This function includes error values and empty text (&quot;&quot;) in the count.|
|Example|<ol><li>Import or create a collection named **Inventory**, as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**CountA(Inventory!UnitsInStock)**<br><br>The label shows **5**, the number of non-empty cells in the **UnitsInStock** column.</li></ol>|

### <a name="countif"></a>CountIf
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**CountIf**(*Table, Expression*)|
|Description|Counts the rows in a table that satisfy the given condition.|
|Example|<ol><li>Import or create a collection named **Inventory**, as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**CountIf(Inventory, UnitsInStock&lt;30)**<br><br>The label shows **2** because two products (Ganymede and Callisto) have fewer than 30 units in stock.</li></ol>|

### <a name="countrows"></a>CountRows
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**CountRows**(*Table*)|
|Description|Counts the rows in a table.|
|Example|<ol><li>Import or create a collection named **Inventory**, as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**CountRows(Inventory)**<br><br>The label shows **5** because the collection contains five rows.</li></ol>|

### <a name="date"></a>Date
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Date**(*Year*, *Month*, *Day*)|
|Description|Returns the sequential serial number that represents the specified date. You can use the DateValue function to customize the date display.<ul><li><em>Year</em><ul><li>If <em>Year</em> is between 0 and 1899 (inclusive), the function adds that value to 1900 to calculate the year.</li><li>If <em>Year</em> is between 1900 and 9999 (inclusive), the function uses that value as the year.</li><li>If <em>Year</em> is less than 0 or is 10000 or greater, the function returns an error value.</li></ul></li><li><em>Month</em><ul><li>If <em>Month</em> is greater than 12, the function adds that number of months to the first month of the specified year.</li><li>If <em>Month</em> is less than 1, the function subtracts that many months, plus 1, from the first month of the specified year.</li></ul></li><li><em>Day</em><ul><li>If <em>Day</em> is greater than the number of days in the specified month, the function adds that many days to the first day of the month and returns the corresponding date from a subsequent month.</li><li>If <em>Day</em> is less than 1, the function subtracts that many days, plus 1, from the first day of the specified month.</li></ul></li></ul>|
|Example|1. Add three input-text controls, and name them **HireMonth**, **HireDay**, and **HireYear**.<br/><br/>2. Add a label, and set its **Text** property to this expression:<br/>**Text(Date(Value(HireYear!Text), Value(HireMonth!Text), Value(HireDay!Text)), "mmmm dd, yyyy")**<br/><br/>3. Press F5, and then type **3** in **HireMonth**, **17** in **HireDay**, and **1979** in **HireYear**.<br/><br/>The label shows **March 17, 1979**.<br/><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="dateadd"></a>DateAdd
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**DateAdd**(*Date*, *NumberOfUnits*[, *Units*])|
|Description|Returns a date that's a specified number of days before or after a specified date. The first argument specifies the original date, and the second argument specifies the number of days to add or subtract. As an alternative, you can use a third optional argument to add or subtract **Months**, **Quarters**, or **Years**.|
|Examples|If today were Oct. 1, 2015, and you set the **Text** property of a label to this expresion:<ul><li>**Text(DateAdd(Today(), 3), "mmm. dd, yyyy")**<br/>The label would show **Oct. 04, 2015**.</li><br><li>**Text(DateAdd(Today(), -3), "mmm. dd, yyyy")**<br/>The label would show **Sep. 28, 2015**.</li><br><li>**Text(DateAdd(Today(), 3, Months), "mmm. dd, yyyy")**<br/>The label would show **Jan. 01, 2016**.</li></ul>[More examples](show-text-dates-times.md) of how to manage dates and times.<br/><br/>

### <a name="datediff"></a>DateDiff
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**DateDiff**(*StartDate*, *EndDate*[, *Units*])|
|Description|Returns the difference between two dates. By default, this function returns the result in **Days**, but you can specify a third argument to return the results in **Years**, **Quarters**, or **Months**.|
|Examples|If today were July 15, 2013,  and you set the **Text** property of a label to this expression:<br><ul><li>**DateDiff(Today(), 1/1/2014)**<br>The label would show **170** as the number of days between today and the first day of the next year.</li><br><li>**DateDiff(Today(), 1/1/2014, Months)**<br>The label would show 6 because the number of months between the dates is more than five and less than seven.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="datetimevalue"></a>DateTimeValue
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**DateTimeValue**(*DateTimeText*)<br><br>**DateTimeValue**(*DateTimeText*, &quot;*LanguageCode*&quot;)||
|Description|Converts a text representation of a date and a time to a value on which you can perform a mathematical or Boolean operation, such as comparing two dates. You can also specify a language code to ensure that a date structured with slashes is interpreted appropriately as MM/DD/YYYY or DD/MM/YYYY.|
|Examples|If you typed 10/11/2014 1:50:24.765 PM into an input-text control named **Start** and then set the **Text** property of a label to this expression:<ul><li>**Text(DateTimeValue(Start!Text), DateTimeFormat!LongDateTime)**<br>The label would show Saturday, October 11, 2014 1:50:24 PM if your computer were set to the &quot;en&quot; locale.<br>**Note:** You can use several options, other than **LongDateTime**, with the **DateTimeFormat** parameter. To display a list of those options, type the parameter, followed immediately by an exclamation point, in the Function Bar.<br><br></li><li>**Text(DateTimeValue(Start!Text, &quot;fr&quot;), DateTimeFormat!LongDateTime)**<br>The label would show Monday, November 10, 2014 1:50:24 PM.<br><br></li><li>**Text(DateTimeValue(Start!Text), &quot;dddd, mmmm dd, yyyy hh:mm:ss.fff AM/PM&quot;)**<br>The label would show Saturday, October 11, 2014 01:50:24:765 PM if your computer were set to the &quot;en&quot; locale.<br><br>**Note:** You can specify **hh:mm:ss.f** or **hh:mm:ss.ff** to round the time to the nearest tenth or hundredth of a second.</li></ul>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="datevalue"></a>DateValue
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**DateValue**(*DateText*)<br>**DateValue**(*DateText*, &quot;*LanguageCode*&quot;)|
|Description|Converts a text representation of a date to a value on which you can perform a mathematical or Boolean operation, such as comparing two dates. The source data must follow one of these patterns:<ul><li>*<em>MM/DD/YYYY</em>*</li><li>*<em>DD/MM/YYYY</em>*</li><li>*<em>DD Mon YYYY</em>*</li><li>*<em>Month DD, YYYY</em>*</li></ul>You can also specify a language code to ensure that a date structured with slashes is interpreted appropriately as MM/DD/YYYY or DD/MM/YYYY.|
|Examples|If you typed 10/11/2014 into an input-text control named **Startdate** and then set the **Text** property of a label to this expression:<ul><li>**Text(DateValue(Startdate!Text), DateTimeFormat!LongDate)**<br>The label would show Saturday, October 11, 2014, if your computer were set to the &quot;en&quot; locale.<br>**Note:** You can use several options, other than **LongDateTime**, with the **DateTimeFormat** parameter. To display a list of those options, type the parameter, followed immediately by an exclamation point, in the Function Bar.<br><br></li><li>**Text(DateValue(Startdate!Text, &quot;fr&quot;), DateTimeFormat!LongDate)**<br>The label would show Monday, November 10, 2014.</li></ul>If you did the same thing on October 20, 2014:<ul><li>**DateDiff(DateValue(Startdate!Text), Today())**<br>If your computer were set to the **en** language code, the label would show 9, indicating the number of days between October 11 and October 20. [DateDiff](#datediff) can also show the difference in months, quarters, or years.</li></ul>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="day"></a>Day
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Day**(*DateTime*)|
|Description|Returns the day from a DateValue function. The returned value can range from 1 to 31.|
|Example|<ol><li>Add an input-text control, and name it **EventDate**.</li><li>Add a label, and set its **Text** property to this expression:<br>**Day(DateValue(EventDate!Text))**</li><li>Type any of these dates into the **EventDate** box:<ul><li>07/15/2013</li><li>15 July 2013</li><li>July 15, 2013</li></ol>The label shows **15**.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="disable"></a>Disable
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Disable**(*Signal*)|
|Description|Disables a signal data source so that an app can't pull signals (data) from it. Location is the only signal data source that this release supports.|
|Example|**Disable(Location)**|

### <a name="distinct"></a>Distinct
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Distinct**(*Table*, *Expression*)|
|Description|Evaluates an expression over one or more columns of a table and returns a one-column table that contains distinct values for the evaluated expression.|
|Example|If you had an Employees table that contained a Department column, this expression would list each unique department name in that column, no matter how many times each name appeared in that column:<br>**Distinct(Employees, Department)**|

### <a name="dropcolumns"></a>DropColumns
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**DropColumns**(*Table*, *Column1*[, *Column2*, …])|
|Description|Returns a table that is based on the specified table but doesn't contain the specified columns.|
|Example|If you had an Employees table that contained a FirstName column, a LastName column, an Address column, and several other columns, this expression would return the same table except without those columns:<br>**DropColumns(Employees, &quot;FirstName&quot;, &quot;LastName&quot;, &quot;Address&quot;)**|

### <a name="enable"></a>Enable
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Enable**(*Signal*)|
|Description|Enables a signal data source so that an app can pull data (signals) from it. Location is the only signal data source that this release supports.|
|Example|**Enable(Location)**|

### <a name="encodeurl"></a>EncodeUrl
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**EncodeUrl**(*Text*)|
|Description|Encodes all instances of non-alphanumeric characters in a string that represents a URL. For example, you can use this function to help create a mail link by merging strings that contain From:, To:, Subject: and Body: fields.|
|Example|If you set the **Text** property of a label to this expression:<br>**EncodeUrl**("http://example/page/url.aspx")<br><br>The label would show this result: <br>**%27http%3A%2F%2Fexample%2Fpage%2Furl.aspx**|

### <a name="filter"></a>Filter
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Filter**(*Table*, *Condition1*[, *Condition2*, ...])|
|Description|Returns the rows in the specified table that satisfy the given conditions. By default, if you specify more than one condition, And (that is, &amp;&amp;) joins are used.|
|Example|If you had an Employees table that contained a Salary column, this function would identify the employees whose salaries were greater than 100,000:<br><br>**Filter(Employees, Salary &gt; 100000)**<br><br>For another example, see "Sort and filter items in the gallery" in [Show images and text in a gallery](show-images-text-gallery-sort-filter.md#).

### <a name="find"></a>Find
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Find**(*FindText*, *WithinText*[, *StartNum*])|
|Description|Indicates where one string appears in another string for the first time. The first argument specifies the string that you want to search for in another string. The second argument specifies the string in which you want to search. You can also include a third optional argument to ignore any instances before a certain location in the string in which you're searching. This function is case-sensitive and returns nothing if the string that you're looking for doesn't appear in the string that you're searching.|
|Example|<ol><li>Add two input-text controls, and name them **SearchFor** and **SearchIn**.</li><br><li>Add a label, and set its **Text** property to this expression:<br>**Find(SearchFor!Text, SearchIn!Text)**</li><br><li>Press F5, type **cab** in the **SearchFor** box, and type or paste **Honorificabilitudinitatibus** in the **SearchIn** box.<br>The label shows **9** because "cab" appears in the search text starting with the ninth character.</li><br><li>Set the **Text** property of the label to this expression:<br>**Find(SearchFor!Text, SearchIn!Text, 10)**.<br>The label doesn't show anything because "cab" doesn't appear in the search text after the 10th character.</li>|

### <a name="first"></a>First
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**First**(*Table*)|
|Description|Returns the first row from the specified table.|
|Example|If you had an Employees table, this function would return the first row from that table:<br><br>**First(Employees)**|

### <a name="firstn"></a>FirstN
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**FirstN**(*Table*[, *NumRows*])|
|Description|Returns the specified number of rows from the beginning of the specified table. The NumRows argument is optional; if it isn't specified, only the first row is returned.|
|Example|If you had an Employees table, this function would return the first 10 rows from that table:<br><br>**FirstN(Employees, 10)**|

### <a name="hashtags"></a>HashTags
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**HashTags**(*Text*)|
|Description|Creates a list of hashtags that start with a pound sign (\#) and contain any combination of these kinds of characters:<ul><li>upper and lowercase letters</li><li>numerals</li><li>underscores (_)</li><li>currency symbols (such as $)</li></ul>Listed hashtags can't contain any other special characters.|
|Example|<ol><li>Add an input-text control, name it **Tweet**, and type or paste this sentence into it:<br>**This #app is #AMAZING and can #coUnt123 or #123abc but not #1-23 or #$*(#@&quot;)**</li><br><li>Add a vertical custom gallery, and set its **Items** property to this function:<br>**HashTags(Tweet!Text)**</li><br><li>Add a label to the gallery template.<br>The label shows these hashtags.<ul><li>**#app**</li><li>**#AMAZING**</li><li>**#coUnt123**</li><li>**#123abc**</li><li>**#1**</li></ul></li></ol>|

### <a name="hour"></a>Hour
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Hour**(*DateTime*)|
|Description|Returns the hour of a given TimeValue as a number between 0 (12:00:00 A.M.) and 23 (11:00:00 P.M.), inclusive.|
|Example|<ol><li>Add an input-text control, and name it **EventTime**.</li><br><li>Add a label, and set its **Text** property to this expression:<br>**Hour(TimeValue(EventTime!Text))**</li><br><li>Press F5, and then type or paste **10:20:30 PM** into the **EventTime** box.<br>The label shows **22**.</li></ol>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="if"></a>If
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**If**(*Condition1*, *Result1*[, *Condition2*, *Result2*, *ConditionN*, *ResultN*, *DefaultResult*])|
|Description|Returns the result that corresponds to the first condition matched. If none of the conditions match, the Default result is returned. If you specify a string as a result, you must surround it with quotation marks.|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><br><li>Set the **Text** property of the lower label in the gallery to this function:<br>**If(UnitsInStock&lt;30, &quot;Order more!&quot;, UnitsInStock)**<br><br>If the number of units in stock is fewer than 30, the label shows the message between the quotation marks. Otherwise, the label shows the number of units in stock.</li></ol>|

### <a name="isblank"></a>IsBlank
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**IsBlank**(*Expression*)|
|Description|Returns true if an expression evaluates to blank (no value); otherwise, returns false. For example, you could combine this function with the If function to notify users when they leave a required field blank.|
|Example|<ol><li>Add an input-text control, and name it **Quantity** (for example, in an order form).</li><br><li>Add a label, and set its **Text** property to this expression:<br>**If(IsBlank(Quantity!Text), &quot;Please specify a quantity.&quot;)**</li><br><li>Press F5, and then type a value in the **Quantity** box.</li>The label stops reminding you to specify a quantity.</ol>|

### <a name="isempty"></a>IsEmpty
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**IsEmpty**(*Source*)|
|Description|Identifies whether a table or a collection contains any data.|
|Example|If a table named Employees contains data, **IsEmpty(Employees)** returns false; otherwise, the function returns true.<br>For another example, see [SaveData](reference-functions.md#savedata).|

### <a name="language"></a>Language
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Language()**|
|Description|Returns the currently active language from the language preferences for an app that hasn't yet been published. If you change the language preference while KratosApps is open, you must restart KratosApps for the function to reflect the change.<br><br>For a published app, this function returns the language with which the app was branded just before it was published.|
|Example|**Language()** could return en-US based on your configuration.|

### <a name="last"></a>Last
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Last**(*Table*)|
|Description|Returns the last row from the specified table.|
|Example|If you had a table named Employees, this function would return the last row from that table:<br>**Last(Employees)**|

### <a name="lastn"></a>LastN
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**LastN**(*Table*[, *NumRows*])|
|Description|Returns the specified number of rows from the end of the table. The *NumRows* argument is optional; if it isn't specified, this function returns only the last row.|
|Example|If you had a table named Employees, this function would return the last 15 rows from that table:<br>**LastN(Employees, 15)**|

### <a name="launch"></a>Launch
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Launch**(*Hyperlink*)|
|Description|Runs the app that's associated with the specified hyperlink and opens the hyperlink itself.|
|Example|<ol><li>Set the **OnSelect** property of a button to this function:<br>**Launch("http://www.bing.com")**</li><br><li>Press F5, and then click the button.<br>The Bing homepage opens.</li></ol>|

### <a name="left"></a>Left
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Left**(*Text*, *NumChars*)<br><br>**Left**(*ColumnExpression*, *NumericExpression*)|
|Description|Returns the specified number of characters from the beginning of the given string.|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **Text** property of the lower label in the gallery to this function:<br>**Left(ThisItem!ProductName, 3)**<br>The label shows the first three characters in each product name.</li></ol>|

### <a name="len"></a>Len
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Len**(*Text*)<br>**Len**(*ColumnExpression*)|
|Description|<ul><li>**Len**(*<em>Text</em>*)<br>Returns the number of characters in a string.</li><li>**Len**(*<em>ColumnExpression</em>*)<br>Given a one-column table of strings, returns a one-column table that contains the corresponding string lengths.</li></ul>|
|Example|<ol><li>Add an input-text control, and name it **Password**.</li><li>Add a label, and set its **Text** property to this expression:<br>**Len(Password!Text)**</li><li>Press F5, and then type or paste **f@V0ritebandname** into the **Password** box.<br>The label shows **16**.|

### <a name="loaddata"></a>LoadData
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**LoadData**(*Collection*, *Filename*)|
|Description|Decrypts the data in the specified file and inserts it into the specified collection. Use this function together with the SaveData function to save and load application data to and from app local storage.<br><br>LoadData is an asynchronous function and can't be used in predicates. We recommend that the result of LoadData be piped into a collection whose schema is known, because LoadData itself doesn't provide a schema.|
|Example|Follow the steps in the example for [SaveData](#savedata).|

### <a name="lookup"></a>LookUp
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**LookUp**(*Table*, *Condition*, *Expression*)|
|Description|This function takes three arguments: a table, a condition that evaluates to true or false for each row in the table, and an expression. For the first row for which the condition evaluates to true, the expression is evaluated, and the result is returned.|
|Example|<ol><li>Import or create a collection named **Inventory** as the first step in the first procedure of [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this expression:<br>**LookUp(Inventory, "Callisto" in ProductName, UnitsInStock)**<br>The label shows the number of units in stock for the product you specified.</li>|

### <a name="lower"></a>Lower
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Lower**(*Text*)<br>**Lower**(*ColumnExpression*)|
|Description|<ul><li>**Lower**(*<em>Text</em>*)<br>Converts the letters in the specified text string to lowercase.</li><li>**Lower**(*<em>ColumnExpression</em>*)<br>Given a one-column table of string values, returns a one-column table of the corresponding lowercase values.</li></ul>|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **Text** property of the lower label in the gallery to this function:<br>**Lower(ThisItem!ProductName)**<br>The label shows the name of each product in all lowercase letters.</li></ol>|

### <a name="max"></a>Max
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Max**(*Table*, *Expression*)<br>**Max**(*Expression1*[, *Expression2*, ...])|
|Description|Returns the largest value among its arguments.|
|Example|<ol><li>Import or create a collection named **Inventory** as the first step in the first procedure of [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**Max(Inventory, UnitsInStock)**<br><br>The label shows the highest value in the **UnitsInStock** column of the **Inventory** collection.</li></ol>|

### <a name="mid"></a>Mid
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Mid**(*Text*, *StartPosition*, *NumChars*)<br><br>**Mid**(*TextColumn*, *StartPositions*, *NumChars*)|
|Description|Returns the characters from a string, given the position of the starting character and the number of characters to extract. You can run this function on a table of strings.|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **Text** property of the lower label in the gallery to this function:<br><br>**Mid(ThisItem!ProductName, 2, 3)**<br><br>The label shows second, third, and fourth letters in the name of each product.</li></ol>|

### <a name="min"></a>Min
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Min**(*Table*, *Expression*)<br><br>**Min**(*Expression1*[, *Expression2*, …])|
|Description|Returns the smallest value among its arguments.|
|Example|<ol><li>Import or create a collection named **Inventory** as the first step in the first procedure of [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a label, and set its **Text** property to this function:<br><br>**Min(Inventory, UnitsInStock)**<br><br>The label shows the lowest value in the **UnitsInStock** column of the **Inventory** collection.</li></ol>|

### <a name="minute"></a>Minute
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Minute**(*DateTime*)|
|Description|Returns the minute from a given TimeValue as a number between 0 and 59 (inclusive).|
|Example|<ol><li>Add an input-text control, and name it **EventTime**.</li><li>Add a label, and set its **Text** property to this expression:<br>**Minute(TimeValue(EventTime!Text))**</li><li>Press F5, and then type **10:20:30 PM** into the **EventTime** box.<br>The label shows **20**.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="month"></a>Month
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Month**(*DateTime*)|
|Description|Returns the month from a given DateValue as a number between 1 and 12 (inclusive).|
|Example|<ol><li>Add an input-text control, and name it **EventDate**.</li><li>Add a label, and set its **Text** property to this expression:<br>**Month(DateValue(EventDate!Text))**</li><li>Type any of these dates into the **EventDate** box:<ul><li>07/15/2013</li><li>15 July 2013</li><li>July 15, 2013</li></ol>The label shows **7**.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="navigate"></a>Navigate
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Navigate**(*TargetScreen*, *Animation*[, *Context*])|
|Description|Changes the view to the specified target screen. These transition animations are supported: ScreenTransition!Cover, ScreenTransition!UnCover, and ScreenTransition!Fade. By specifying a *Context* argument, you can pass a state/context record to the target screen that it can then use to guide its computations. The target screen has unqualified access to the fields in the context record.<br><br><blockquote><p>[AZURE.IMPORTANT] If you pass a <em>Context/<em> record to a target screen, its own context may be modified.</p></blockquote>|
|Example|<ol><li>Name the default screen **DefaultScreen**, and add a label to it so that you can verify which screen is showing in **Preview**.</li><li>Add a second screen, name it **AddlScreen**, and add a label to it.</li><li>Add a button to **DefaultScreen**, and set its **OnSelect** property to this function:<br><br>**Navigate(AddlScreen, ScreenTransition!Fade)**</li><li>From the **DefaultScreen**, press F5, and then click the button.<br><br>**AddlScreen** appears.</li></ol>|

### <a name="not"></a>Not
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Not**(*BooleanExpression*)|
|Description|Computes the logical negation of a Boolean expression.|
|Example**<br><br>This function makes sure a radio button isn't selected:|**Not(RadioButton1!Selected)**|

### <a name="now"></a>Now
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Now()**||
|Description|Returns the current date and time in the device's locale-specific format. To format it, use the [Text](#text) function.|
|Example|If today were October 11, 2014, at exactly 3:25 PM and you set the text property of a label to **Text(Now(), &quot;mm/dd/yyyy hh:mm:ss.fff&quot;)**, the label would show 10/11/2014 3:25:00:000 PM if your computer were set to the **en** language code. The label would show 11/10/2014 3:25:00:000 PM if your computer were set to the **fr** language code.<br><br>As an alternative, you can specify **hh:mm:ss.f** or **hh:mm:ss.ff** to round the time to the nearest tenth or hundredth of a second.<br><br>If fractions of seconds don't matter in your app, you can use the DateTimeFormat parameter to specify the date, time, or both in any of several built-in formats. For example, you can replace the function in this example with **Text(Now(), DateTimeFormat!ShortDateTime)** to get the same results but without the milliseconds. To display a list of options for this parameter, type it, immediately followed by an exclamation mark, in the function box.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="or"></a>Or
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Or**(*LogicalExpression1*[, *LogicalExpression2*, ...])|
|Description|Returns true if any specified expression is true; otherwise, returns false. In contrast, the And function returns true only if all specified expressions are true.<br><br>The Or function accomplishes the same outcome as using the inline **&#124;&#124;** operator.|
|Example|You can use this function to determine whether a slider's value falls outside the 50 to 100 range:<br><br>**Or(Slider1!Value &lt; 50, Slider1!Value&gt; 100)**<br><br>If a table contained a Dept column and a Salary column, you could use this function in a Result column to show true in all rows in which the value in the Dept column was HR or the value in the Salary column was larger than 200000:<br><br>**Or(Dept = HR, Salary &gt;= 200000)**<br><br>As an alternative, you can use the **&#124;&#124;** operator to get the same results as what the previous functions return:<br><br>**Slider1!Value &lt; 50 &#124;&#124; Slider1!Value&gt; 100**<br><br>**Dept = &quot;HR&quot; &#124;&#124; Salary &gt; 200000**|

### <a name="plaintext"></a>PlainText
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**PlainText(*TextWithTags*)**|
|Description|Strips HTML and XML tags from text or converts the tags to an appropriate symbol.|
|Example|If you bind a text gallery to an RSS feed and then set the Text property (in the Data category) of a label in that gallery to ThisItem!description, the label might show raw HTML or XML code as in this example:<br><br>&lt;p&gt;We have done an unusually&amp;nbsp;&amp;quot;deep&amp;quot; globalization and localization.&lt;p&gt;<br><br>If you set the Text property of the label to **PlainText(ThisItem!description)**, the text appears as in this example:<br><br>We have done an unusually &quot;deep&quot; globalization and localization.|

### <a name="proper"></a>Proper
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Proper**(*Text*)<br><br>**Proper**(*ColumnExpression*)|
|Description|Converts words in a text string to proper case; that is, the first letter in every word is uppercase, and the other letters are lowercase.<ul><li>**Proper**(*Text*)<br>Converts a string to proper case.</li><li>**Proper**(*<em>Expression</em>*)<br>Given a one-column table of string values, returns a one-column table that contains the corresponding proper-case values.<br><br></li></ul>|
|Example|<ol><li>Add an input-text control, and name it <em>Slogan</em>.<br></li><li>Add a label, and set its <em>Text</em> property to this function:<br><br><em>Proper(Slogan!Text)</em><br><br>If you type &quot;WE ARE THE BEST!&quot; into the text-input control, the label shows &quot;We Are The Best!&quot;</li></ol>|

### <a name="rand"></a>Rand
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Rand()**|
|Description|Returns a pseudo-random number that's greater than or equal to 0 but less than 1.|
|Example|**Rand()** could return 0.85116235, 0.76728732, 0.27591115, or any other number greater than or equal to 0 but less than 1.|

### <a name="refresh"></a>Refresh
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Refresh**(*ServiceDataSource*)|
|Description|Refreshes the data from the specified data source so that the app has the most recent state.<br><br><blockquote><p>[AZURE.IMPORTANT] You can't use this function to refresh data from Excel tables. </p></blockquote>|
|Example|If you added an RSS feed named **rss_1**, **Refresh(rss_1)** would refresh that feed.|

### <a name="remove"></a>Remove
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Remove**(*Collection*, *Record1*[, *Record2*, ..., **All**])<br><br>**Remove**(*Collection*, *Table*[, **All**])|
|Description|Removes one or more rows from a collection. Because a collection can have duplicate records, this function also accepts an optional argument All that removes duplicates.<br><br><blockquote><p>[AZURE.IMPORTANT] This function modifies the underlying collection.</p></blockquote>|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **OnSelect** property of the image in the gallery to this function:<br><br>**Remove(Inventory, ThisItem)**<br></li><li>Press F5, and then click an image in the gallery.<br><br>The item is removed from the gallery and the collection.</li></ol>|

### <a name="removeif"></a>RemoveIf
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**RemoveIf**(*Collection*, *Condition1*[, *Condition2* ...])|
|Description|Removes from a collection all rows that satisfy the specified conditions and returns the modified collection.|
|Example|If you had a collection named ShoppingCart that contained a field named Price, this function would remove from the collection any item for which the price was more than 200.<br><br>**RemoveIf(Cart, Price &gt; 200)**|

### <a name="renamecolumns"></a>RenameColumns
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**RenameColumns(***CollectionName***, &quot;***OldName***&quot;, &quot;***NewName***&quot;)**|
|Description|Creates a temporary table that contains the same data as a data source except that one column has a different name. You can rename columns in a collection or in data imported from, for example, Excel or a SharePoint list.|
|Example|<ol><li>Import or create a collection named **Inventory** as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add an image gallery with text, name it **TableHolder**, and set its **Items** property to this function:<br><br>**RenameColumns(Inventory, &quot;ProductName&quot;, &quot;JacketID&quot;)**</li><li>Add a button, and set its **OnSelect** property to this function:<br><br>**Collect(Inventory2, TableHolder!AllItems)**</li><li>Press F5, click the button you just created, and then press Esc to return to the design workspace.</li><li>Press Alt-D, and then click **Collections** in the left navigation bar.</li><li>Confirm that you've duplicated the **Inventory** collection, except that the new collection, named **Inventory2**, contains the same information in a column named **JacketID** as the original collection did in a column named **ProductName**.</li></ol>|

### <a name="replace"></a>Replace
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Replace**(*Text*, *StartIndex*, *Count*, *NewText*)<br><br>**Replace**(*Column*, *StartIndex*, *Count*, *NewText*)|
|Description|Replaces part of a text string with a different text string, given the position of the starting character and the number of characters to replace. You can run this function on a table of strings.|
|Example|<ol><li>Import or create a collection named **Inventory** as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add an image gallery with text, and set its **Items** property to this function:<br><br>**Replace(Inventory!ProductName, 3, 2, &quot;zz&quot;)**<br><br>In each product name, &quot;zz&quot; replaces the third and fourth letters.</li></ol>|

### <a name="rgba"></a>RGBA
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**RGBA**(*Red*, *Green*, *Blue*, *Alpha*)|
|Description|Returns a color value that has the specified red, green, blue, and alpha components.|
|Example|Add a label, and set its **Color** property to this function:<br><br>**RGBA(112, 48, 160, 1)**<br><br>The text of the label becomes purple.|

### <a name="right"></a>Right
|&nbsp;|&nbsp;|
|---|---|
|Syntax|Right**(*Text*, *NumChars*)<br><br>**Right**(*ColumnExpression*, *NumericExpression*)|
|Description|Returns the specified number of characters from the end of the given string.|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **Text** property of the lower label in the gallery to this function:<br><br>**Right(ThisItem!ProductName, 3)**<br><br>The label shows the last three characters in each product name.</li></ol>|

### <a name="round"></a>Round
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Round**(*Number*, *DecimalPlaces*)<br><br>**Round**(*Column*, *DecimalPlaces*)|
|Description|Rounds the given number to the specified number of decimal places. You can run this function on a table of numbers.|
|Examples|To use this function with data that you provide manually:<br/><br/><ol><li>Add an input-text control, and name it Decimal.<br></li><li>Add a label, and set its Text property to this function:</li><li>**Round(Value(Decimal!Text), 2)**<br></li><li>In the text-input control, type a decimal value such as .634 or .635, and confirm that the label shows the appropriate value (for example, .63 or .64).</li></ol>|

### <a name="rounddown"></a>RoundDown
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**RoundDown**(*Number*, *DecimalPlaces*)<br><br>**RoundDown**(*Column*, *DecimalPlaces*)|
|Description|Rounds down the given number to the specified number of decimal places.|
|Example|RoundDown(23.54, 0)** returns 23.|

### <a name="roundup"></a>RoundUp
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**RoundUp**(*Number*, *DecimalPlaces*)<br><br>**RoundUp**(*Column*, *DecimalPlaces*)|
|Description|Rounds up the given number to the specified number of decimal places.|
|Example|RoundUp(23.44, 1)** returns 23.5.|

### <a name="savedata"></a>SaveData
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**SaveData**(*Collection*, *FileName*)|
|Description|Encrypts the data in the specified collection and saves it to the specified file. This file is located in the app's own protected space. Use this function together with the **LoadData** function to save and load application data to and from app local storage.<br><br>SaveData is an asynchronous function and can't be used in predicates such as predicates of Filter and CountIf.|
|Example|1. [Create a collection](create-update-collection.md) that has one column.<br>2. Change the **OnSelect** property of the button to this expression:<br>**Collect(Destinations, Destination!Text);SaveData(Destinations, "destfile")**<br>3. Click a blank area of the screen to select it, and then set its **OnVisible** property to this expression:<br/>**If(IsEmpty(Destinations), LoadData(Destinations, "destfile"))**<br><br>Step 2 saves the collection whenever a destination is added. Step 3 loads the data into the collection but only if it's empty when the screen appears.<br/><ul><li>When you close and reopen an app, all collections are empty by default, so the app can't show your saved data. In that case, the saved data is loaded when the screen appears.</li><li>If the app has multiple screens and you navigate to that screen from another screen, the collection might already contain data. If it does, the expression does nothing so that it doesn't create duplicates.|

### <a name="second"></a>Second
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Second**(*DateTime*)|
|Description|Returns the second from a given TimeValue as a number between 0 and 59 (inclusive).|
|Example|If you typed 10:20:30 PM into an input-control named EventTime, a label would show 30 if its text property were set to **Second(TimeValue(EventTime!Text))**.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="showcolumns"></a>ShowColumns
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**ShowColumns(***CollectionName*, &quot;*Column1*&quot;, &quot;*Column2*&quot;...**)**|
|Description|Creates a temporary table that contains only the columns that you specify from a data source that you specify. You can specify columns from a collection or data imported from, for example, Excel or a SharePoint list.|
|Examples|<ol><li>Import or create a collection named **Inventory** as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Add a text gallery, name it **TableHolder**, and set its **Items** property to this function:<br><br>**ShowColumns(Inventory, &quot;ProductName&quot;, &quot;UnitsInStock&quot;)**</li><li>Add a button, and set its **OnSelect** property to this function:<br><br>**Collect(Inventory2, TableHolder!AllItems)**</li><li>Press F5, click the button you just created, and then press Esc to return to the design workspace.</li><li>Press Alt-D, and then click **Collections** in the left navigation bar.</li><li>Confirm that you've created a collection, named **Inventory2**, that contains the **ProductName** and **UnitsInStock** columns (but not the **ProductDesign** column) from the **Inventory** collection.</li></ol>|

### <a name="shuffle"></a>Shuffle
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Shuffle**(*Collection*)|
|Description|Returns a copy of the given collection, in which rows in the table are randomly reordered.|
|Example|If you stored details about playing cards in a collection named Deck, this function would shuffle that collection:<br><br>**Shuffle(Deck)**|

### <a name="sort"></a>Sort
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Sort**(*Table*, *Expression*[, **SortOrder!Descending**])|
|Description|Returns a copy of a collection, in which the rows in the given table are sorted based on the result of the specified expression evaluated to one of the supported expression types—number and its subtypes, string and its subtypes, and Boolean types. The function doesn't support sorting on aggregate values such as table and rows. The function also accepts an optional argument that indicates that the table should be sorted in descending order.|
|Example|[Show data in a gallery](show-images-text-gallery-sort-filter.md) for an example.|

### <a name="sqrt"></a>Sqrt
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Sqrt**(*Number*)<br><br>**Sqrt**(*ColumnExpression1*)|
|Description|Returns the square root of a positive number. You can run this function on a table of numbers.|
|Examples|<ol><li>Add an input-text control, and name it **Source**.<br></li><li>Add a label, and set its **Text** property to this function:<br><br>**Sqrt(Value(Source!Text))**<br></li><li>Type a number into the input-text control, and confirm that the label shows the square root of the number that you typed.</li></ol>|

### <a name="stdevp"></a>StdevP
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**StdevP**(*Table*,*Expression*)<br><br>**StdevP**(*Expression1*[,*Expression2*, ...])|
|Description|Returns the standard deviation of its arguments.|
|Examples|If you had a Sales table that not only contained a CostPerUnit column and a UnitsSold column but also listed each region on a different row, this function would compute standard deviation of sales by region:<br><br>**StdevP(Sales, CostPerUnit * UnitsSold)**<br><br>To compute the standard deviation of the values set for sliders 1 through 7:<br><br>**StdevP(Slider1!Value, Slider2!Value, Slider3!Value, Slider4!Value, Slider5!Value, Slider6!Value, Slider7!Value)**|

### <a name="substitute"></a>Substitute
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Substitute**(*Text*, *OldText*, *NewText*[,*InstanceNum*])<br><br>**Substitute**(*TextColumn*, *OldTextColumn*, *NewTextColumn*[, *InstanceNumColumn*])|
|Description|Replaces part of a text string with a different text string. If the optional fourth argument is used, it specifies the instance to match and replace, starting with 1, which means the first instance.|
|Example|This function replaces &quot; &amp; &quot; with &quot; and &quot;:<br><br>**Substitute(Text1!Text, &quot; &amp; &quot;, &quot; and &quot;)**|

### <a name="sum"></a>Sum
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Sum**(*Table*, *Expression*)<br><br>**Sum**(*Expression1*[, *Expression2*, ...])|
|Description|Returns the sum of the arguments, for the specified range.|
|Examples|If you had a table named Sales that contained a CostPerUnit column and a UnitsSold column, this function would compute total sales:<br><br>**Sum(Sales, CostPerUnit * UnitsSold)**<br><br>To compute the sum of the values set for sliders 1, 2, and 3:<br><br>**Sum(Slider1!Value, Slider2!Value, Slider3!Value)**|

### <a name="table"></a>Table
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Table**({*Column1*:*Row1*, *Column2*:*Row1*...}, {*Column1*:*Row2*, *Column2*:*Row2*...})|
|Description|Creates a temporary table that contains the data that you specify. You don't have to specify data in every column for every row.|
|Examples|<ul><li>Add a listbox, and then set its **Items** property to this function:<br><br>**Table({Color:&quot;red&quot;}, {Color:&quot;green&quot;}, {Color:&quot;blue&quot;})**</li><li>Add a text gallery, and set its **Items** property to this function:<br><br>**Table({Item:&quot;Violin123&quot;, Location:&quot;France&quot;, Owner:&quot;Fabrikam&quot;}, {Item:&quot;Violin456&quot;, Location:&quot;Chile&quot;})**<br><br>(optional) Set the **Text** property of the **Heading1** label to **ThisItem!Item**, set the **Text** property of the **Subtitle1** label to **ThisItem!Owner**, and set the **Text** property of the **Body1** label to **ThisItem!Location**.</li></ul>|

### <a name="text"></a>Text
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Text**(*Value*, *Format*)|
|Description|Converts a value to a formatted text output.|
|Examples|<ol><li>Add a text-input control, name it **Source**, and then type **56.75** in it.</li><li>Add a label, and set its **Text** property to this expression:<br><br>**Text(Value(Source!Text), &quot;$#.##&quot;)**<br><br>The label shows **$56.75**.</li><li>Change the **Text** property of the label to this expression:<br><br>**Text(Value(Source!Text), &quot;#.##%&quot;)**<br><br>The label shows **56.75%**.</li></ol><a href="https://technet.microsoft.com/library/dn955337(v=vs.111).aspx">Format dates and times</a>.|

### <a name="time"></a>Time
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Time**(*Hour*, *Minute*, *Second*)|
|Description|Converts the specified hours, minutes, and seconds into a decimal.|
|Example|If a user typed 14 in an input-text control named BirthHour, 50 in an input-text control named BirthMinute, and 24 in an input-text control named BirthSecond, this function would return 02:50:24 p.<br><br>**Text(Time(Value(BirthHour!Text), Value(BirthMinute!Text), Value(BirthSecond!Text)), &quot;hh:mm:ss a/p&quot;)**<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="timevalue"></a>TimeValue
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**TimeValue**(*TimeText*)<br><br>**TimeValue**(*TimeText*, &quot;*LanguageCode*&quot;)|
|Description|Converts a time value stored as text to a value on which you can perform a mathematical or Boolean operation, such as comparing two times. For consistency, all times are converted from the local time zone to UTC (Coordinated Universal Time). As a result, a user in the Pacific time zone might specify 1:50:24 PM, a user in the Eastern time zone might specify 4:50:24 PM, and both values would appear as 5:50:24 AM.<br><br>You can also specify a language code to ensure that a time value is interpreted and formatted appropriately.|
|Example|Name an input-text control **FinishedAt**, and set the **Text** property of a label to this function:<br><br>**If(TimeValue(FinishedAt!Text)&lt;TimeValue(&quot;5:00:00.000 PM&quot;), &quot;You made it!&quot;, &quot;Too late!&quot;)**<ul><li>If you type 4:59:59.999 PM into the **FinishedAt** control, the label shows **&quot;You made it!&quot;**</li><li>If you type 5:00:00.000 PM into the **FinishedAt** control, the label shows **&quot;Too late!&quot;**</li></ul>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="today"></a>Today
|&nbsp;|&nbsp;|
|---|---|
|Syntax|Today()|
|Description|Returns the current date, in the device's locale-specific format.|
|Example|If today were October 11, 2014, and you set the Text property of a label tothis function:<ul><li>**Today()**<br><br>The label would show 10/11/2014 12:00 AM if your computer were set to the **en** language code or 11/10/2014 12:00 AM if your computer were set to the **fr** language code.</li><li>**Text(Today(), &quot;mm/dd/yyyy&quot;)**<br><br>The label would show 10/11/2014 regardless of the language code to which your computer was set.</li><li>**T**ext(Today(), DateTimeFormat!ShortDate)**<br><br>The label would show 10/11/2014 regardless of the language code to which your computer was set.<br><br>You can use several options, other than ShortDate, with the **DateTimeFormat** parameter. To display a list of those options, type the parameter, followed immediately by an exclamation point, in the function box.</li></ul>[More examples](show-text-dates-times.md) of how to manage dates and times.|

### <a name="trim"></a>Trim
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Trim**(*Text*)<br><br>**Trim**(*ColumnExpression*)|
|Description|Removes all spaces from a text string except for single spaces between words.|
|Examples|If you typed &quot;We are    the best!&quot; into an input-text control named Slogan, a label with a text property of **Trim(Slogan!Text)** would return &quot;We are the best!&quot;|

### <a name="update"></a>Update
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Update**(*Collection*, *Record1*, *Record2*[, &quot;**All**&quot;])|
|Description|In a specified collection, replaces the matching record with the specified record and returns the resulting collection. To update all matches, specify the optional argument &quot;All&quot;.<br/><br/><blockquote><p>[AZURE.IMPORTANT] This function modifies the underlying collection</p></blockquote>|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Name the gallery **ProductGallery**.</li><li>Add a slider named **UnitsSold**, and set its **Max** property to this expression:<br>**ProductGallery!Selected!UnitsInStock**</li><li>Add a button, and set its **OnSelect** property to this expression:<br>**Update(Inventory, {ProductDesign:ProductGallery!Selected!ProductDesign, ProductName:ProductGallery!Selected!ProductName, UnitsInStock:ProductGallery!Selected!UnitsInStock}, {ProductDesign:ProductGallery!Selected!ProductDesign, ProductName:ProductGallery!Selected!ProductName, UnitsInStock:ProductGallery!Selected!UnitsInStock-UnitsSold!Value})**</li><li>Press F5, click a product in the gallery, specify a value with the slider, and then click the button.<br>The number of units in stock decreases by the amount that you specified.</li></ol>|

### <a name="updatecontext"></a>UpdateContext
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**UpdateContext**({*Name1*: *Expression1*, *Name2*: *Expression2*, …})|
|Description|Updates the context of the current screen and binds the specified variables to the results from the evaluation of the specified expressions.<br/><br/><blockquote><p>[AZURE.IMPORTANT]This function modifies the underlying screen context.</p></blockquote>|
|Example|UpdateContext({page: 5, displayItem: &quot;Tablets&quot;})|

### <a name="updateif"></a>UpdateIf
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**UpdateIf**(*Collection*, *Condition1*, {*Column1*: *Expression1*, …}[, *Condition2*, {*Column1*: *Expression2*, …} …])|
|Description|Updates the specified columns by using the results of the corresponding expressions for the rows that satisfy the specified conditions, and returns the modified collection.<br/><br/><blockquote><p>[AZURE.IMPORTANT] This function modifies the underlying collection.</p></blockquote>|
|Example|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Name the gallery **ProductGallery**.</li><li>Add a slider named **UnitsSold**, and set its **Max** property to this expression:<br>**ProductGallery!Selected!UnitsInStock**</li><li>Add a button, and set its **OnSelect** property to this expression:<br>**UpdateIf(Inventory, ProductName = ProductGallery!Selected!ProductName, {UnitsInStock:UnitsInStock-UnitsSold!Value})**</li><li>Press F5, click a product in the gallery, specify a value with the slider, and then click the button.<br>The number of units in stock for the product you specified decreases by the amount that you specified.</li></ol>|

### <a name="upper"></a>Upper
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Upper**(*Text*)<br><br>**Upper**(*ColumnExpression*)|
|Description|<ul><li>**Upper**(<em>Text</em>)<br>Converts the letters in the specified text string to uppercase.</li><li>**Upper** (<em>ColumnExpression</em>)<br>Given a one-column table of string values, returns a one-column table of the corresponding uppercase values.</li></ul>|
|Examples|<ol><li>Import or create a collection named **Inventory**, and show it in a gallery as [Show data in a gallery](show-images-text-gallery-sort-filter.md) describes.</li><li>Set the **Text** property of the lower label in the gallery to this function:<br><br>**Upper(ThisItem!ProductName)**<br><br>The label shows the name of each product in all capital letters.</li></ol>|

### <a name="value"></a>Value
|&nbsp;|&nbsp;|
|---|---|
|Syntax|Value(*Text*)|
|Description|Converts a text string that represents a value to an actual value.|
|Example|1. Add a text-input control, and name it **Price**.<br/>2. Add a label, and set its **Text** property to this expression:<br/>**Text(Value(Price!Text), "$#")**<br/>3. Press F5, and then type a number in the **Price** control.<br/>The label automatically shows the value as a dollar amount.|

### <a name="varp"></a>VarP
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**VarP**(*Table*, *Expression*)<br><br>**VarP**(*Expression1*[, *Expression2*, ...])|
|Description|Returns the variance of its arguments.|
|Examples|If you had a Sales table that not only contained a CostPerUnit column and a UnitsSold column but also listed each region in a different row, this function would compute variance of sales by region:<br><br>**VarP(Sales, CostPerUnit * UnitsSold)**<br><br>To compute the standard deviation of the values set for sliders 1 through 7:<br><br>**VarP(Slider1!Value, Slider2!Value, Slider3!Value, Slider4!Value, Slider5!Value, Slider6!Value, Slider7!Value)**|

### <a name="year"></a>Year
|&nbsp;|&nbsp;|
|---|---|
|Syntax|**Year**(*DateTime*)|
|Description|Returns the year of a given date as a number between 1900 and 9999 (inclusive).|
|Example|Year(DateValue(&quot;03/17/1979&quot;))** returns 1979.<br><br>[More examples](show-text-dates-times.md) of how to manage dates and times.|