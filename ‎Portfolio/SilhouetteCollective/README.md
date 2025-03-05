<a name="top"></a>

[<img src="https://user-images.githubusercontent.com/91146906/152112781-2de05074-70b1-436b-9bfb-860890cc1de1.svg" height="35"/>](../#OLAP)
<hr>

# Silhouette Collective: A Fashion Concierge Business
[<img src="https://user-images.githubusercontent.com/91146906/152239160-8f8c18a2-e724-4be7-863d-bc94151212ce.svg" height="35"/>](#Introduction)
[<img src="https://user-images.githubusercontent.com/91146906/152279618-21ae078d-3d0b-45ed-95f1-306e5030f301.svg" height="35"/>](#BusinessRequirements)
[<img src="https://user-images.githubusercontent.com/91146906/152279677-02eb9847-1863-4641-b59c-58a0e6cd2f24.svg" height="35"/>](#DataMartDesign)
[<img src="https://user-images.githubusercontent.com/91146906/161397549-071ca628-25fa-4c34-91d1-78274cafc9b8.svg" height="35"/>](#PowerBI)

<a name="ExecutiveSummary"></a>
<hr>

## Introduction
Silhouette Collective is a fashion concierge business that provides a highly personalized shopping experience to each and every customer. We collect personal information from each client, such as their clothing sizes, brand preferences, favorite colors, and item preferences to create a customer profile that is assigned to one of our experienced shoppers within the company. The shopper can then shop for specific events or just singular items per the customer’s request. As a new company, we have decided to perform this analysis to get a feel for our earnings and scope within the market thus far. This analysis offers key insights into our performance across various products, markets nationwide, and earnings by product. We can use these key insights to drive our future business decisions surrounding expansion into more markets, our product offerings, as well as our criteria for selecting clothing. As our stakeholders, we hope this analysis reassures you of our potential as a business and our bright future within the online shopping industry. While we have had many successes, as seen in this analysis there is always room for improvement and we look forward to expanding Silhouette Collective and furthering our success.
<br>
<br>The creation of a Silhouette Collective database gives Silhouette Collective a look into customer insights, process optimization, and data-driven decision-making insights to compete in an increasingly competitive industry and to maximize their company potential. We created a data mart to be able to optimize reporting, archive their data, as well as consolidate their large amount of data.
<br>
<br>[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)

<a name="BusinessRequirements"></a>
<hr>

## Business Requirements
<b>Chief Operating Officer (COO):</b> <i>What item brought in the most profit?</i>
<blockquote>This analysis will allow the COO to understand demand for products, as well as which products are actually being purchased most frequently. This informs decisions regarding what products should be in stock and their quantity.</blockquote>

<b>Chief Marketing Officer (CMO):</b> <i>Which shopper generated the highest revenue?</i>
<blockquote>This analysis will inform the CMO of which customers are purchasing from them most frequently. This provides insights into the target demographic and allows the company to market specific promotions to its largest customers.</blockquote>

<b>Chief Executive Officer (CEO):</b> <i>Which year generated the most profit?</i>
<blockquote>This analysis will inform the CEO of which year they have performed the best, allowing them to then look further in to see why that is. This provides insights into what drives profit for the company.</blockquote>

<b>Chief Marketing Officer (CMO):</b> <i>What region generated the most revenue?</i>
<blockquote>This analysis will allow the CMO to understand the order placement habits in terms of regions in the US. This information will inform marketing and promotion decisions to establish continued loyalty in regions seeing high , in addition to the development of the business in regions where they are seeing less purchases.</blockquote>

<br>[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)

<a name="DataMartDesign"></a>
<hr>

## Data Mart Design
### Information Package

<table>
  <tr>
    <td colspan="6">&nbsp;<i>Dimensions</i></td>
  </tr>
  <tr>
    <td rowspan="0">&nbsp;<i>Hierarchies</i</td>
  </tr>
  <tr>
    <th>Date</th>
    <th>Shopper</th>
    <th>Item</th>
    <th>Customer</th>
    <th>EventType</th>
  </tr>
  <tr>
    <td>Year</td>
    <td>ShopperID</td>
    <td>ItemID</td>
    <td>CustomerID</td>
    <td>EventTypeID</td>
  </tr>
  <tr>
    <td>Quarter</td>
    <td>Shopper Name</td>
    <td>ItemName</td>
    <td>CustomerName</td>
    <td>EventTypeName</td>
  </tr>
  <tr>
    <td>Month</td>
    <td></td>
    <td>Color</td>
    <td>Size</td>
    <td>EventType</td>
  </tr>
  <tr>
    <td>Date</td>
    <td></td>
    <td>BrandName</td>
    <td>MainColorPref</td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td>ItemPreference</td>
    <td>SecondColorPref</td>
    <td></td>
  </tr>
  <tr>
    <td colspan="5">&nbsp;<b>Fact:</b> Purchase Table- OrderID, ShopperID, CustomerID, OrderDateID, OrderTotal, UnitPrice, UnitCost, Revenue, Cost, Profit</td>
  </tr>
</table>

### Star Schema

![image](https://github.com/user-attachments/assets/8618f936-195a-4992-8e8d-126c16393cf3)


[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)
	
<a name="ETL"></a>
<hr>
	
## Extract, Transform, and Load the Data Mart
Using Visual Studio, we can extract data from the Silhouette Collective Database, transform, and load it into the data mart.

### DimDate
--Load DimDate adapted by Liang Lu for Data Warehousing course using several online resources. Adapted on Feb 11 2019. 
--https://www.codeproject.com/Articles/647950/Create-and-Populate-Date-Dimension-for-Data-Wareho, 
--https://ask.sqlservercentral.com/questions/112546/how-to-derive-season-in-a-date-dimension.html
--Modified by Christopher Pena
```sql
USE SilhouetteCollectiveDM

--Specify Start Date and End date here,based on your business requirements
--Value of Start Date Must be Less than Your End Date 

DECLARE @StartDate DATETIME = '01/01/2019' --Starting value of Date Range
DECLARE @EndDate DATETIME = '12/31/2099' --End Value of Date Range

--Temporary Variables To Hold the Values During Processing of Each Date of Year

DECLARE
	@DayOfWeekInMonth INT,
	@DayOfWeekInYear INT,
	@DayOfQuarter INT,
	@WeekOfMonth INT,
	@CurrentYear INT,
	@CurrentMonth INT,
	@CurrentQuarter INT

/*Table Data type to store the day of week count for the month and year*/

DECLARE @DayOfWeek TABLE (DOW INT, MonthCount INT, QuarterCount INT, YearCount INT)

INSERT INTO @DayOfWeek VALUES (1, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (2, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (3, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (4, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (5, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (6, 0, 0, 0)
INSERT INTO @DayOfWeek VALUES (7, 0, 0, 0)

--Extract and assign various parts of Values from Current Date to Variable

DECLARE @CurrentDate AS DATETIME = @StartDate
SET @CurrentMonth = DATEPART(MM, @CurrentDate)
SET @CurrentYear = DATEPART(YY, @CurrentDate)
SET @CurrentQuarter = DATEPART(QQ, @CurrentDate)

/********************************************************************************************/
--Proceed only if Start Date(Current date ) is less than End date you specified above

WHILE @CurrentDate <= @EndDate
BEGIN
 
/*Begin day of week logic*/

         /*Check for Change in Month of the Current date if Month changed then 
          Change variable value*/
	IF @CurrentMonth != DATEPART(MM, @CurrentDate) 
	BEGIN
		UPDATE @DayOfWeek
		SET MonthCount = 0
		SET @CurrentMonth = DATEPART(MM, @CurrentDate)
	END

        /* Check for Change in Quarter of the Current date if Quarter changed then change 
         Variable value*/

	IF @CurrentQuarter != DATEPART(QQ, @CurrentDate)
	BEGIN
		UPDATE @DayOfWeek
		SET QuarterCount = 0
		SET @CurrentQuarter = DATEPART(QQ, @CurrentDate)
	END
       
        /* Check for Change in Year of the Current date if Year changed then change 
         Variable value*/
	

	IF @CurrentYear != DATEPART(YY, @CurrentDate)
	BEGIN
		UPDATE @DayOfWeek
		SET YearCount = 0
		SET @CurrentYear = DATEPART(YY, @CurrentDate)
	END
	
        -- Set values in table data type created above from variables 

	UPDATE @DayOfWeek
	SET 
		MonthCount = MonthCount + 1,
		QuarterCount = QuarterCount + 1,
		YearCount = YearCount + 1
	WHERE DOW = DATEPART(DW, @CurrentDate)

	SELECT
		@DayOfWeekInMonth = MonthCount,
		@DayOfQuarter = QuarterCount,
		@DayOfWeekInYear = YearCount
	FROM @DayOfWeek
	WHERE DOW = DATEPART(DW, @CurrentDate)
	
/*End day of week logic*/


/* Populate Your Dimension Table with values*/
	
	INSERT INTO [dbo].[DimDate]
	SELECT
		
		CONVERT (char(8),@CurrentDate,112) as DateKey,
		@CurrentDate AS Date,
		CONVERT (char(10),@CurrentDate,101) as FullDate,
		DATEPART(DD, @CurrentDate) AS DayOfMonth,
		DATENAME(DW, @CurrentDate) AS DayName,
		DATEPART(DW, @CurrentDate) AS DayOfWeek,
		@DayOfWeekInMonth AS DayOfWeekInMonth,
		@DayOfWeekInYear AS DayOfWeekInYear,
		@DayOfQuarter AS DayOfQuarter,
		DATEPART(DY, @CurrentDate) AS DayOfYear,
		DATEPART(WW, @CurrentDate) + 1 - DATEPART(WW, CONVERT(VARCHAR, 
		DATEPART(MM, @CurrentDate)) + '/1/' + CONVERT(VARCHAR, 
		DATEPART(YY, @CurrentDate))) AS WeekOfMonth,
		(DATEDIFF(DD, DATEADD(QQ, DATEDIFF(QQ, 0, @CurrentDate), 0), 
		@CurrentDate) / 7) + 1 AS WeekOfQuarter,
		DATEPART(WW, @CurrentDate) AS WeekOfYear,
		DATEPART(MM, @CurrentDate) AS Month,
		DATENAME(MM, @CurrentDate) AS MonthName,
		CASE
			WHEN DATEPART(MM, @CurrentDate) IN (1, 4, 7, 10) THEN 1
			WHEN DATEPART(MM, @CurrentDate) IN (2, 5, 8, 11) THEN 2
			WHEN DATEPART(MM, @CurrentDate) IN (3, 6, 9, 12) THEN 3
			END AS MonthOfQuarter,
		DATEPART(QQ, @CurrentDate) AS Quarter,
		CASE DATEPART(QQ, @CurrentDate)
			WHEN 1 THEN 'Q1'
			WHEN 2 THEN 'Q2'
			WHEN 3 THEN 'Q3'
			WHEN 4 THEN 'Q4'
			END AS QuarterName,
		DATEPART(YEAR, @CurrentDate) AS Year,
		'CY ' + CONVERT(VARCHAR, DATEPART(YEAR, @CurrentDate)) AS CYearName,
		'FY ' + RIGHT(CONVERT(VARCHAR, DATEPART(YEAR, @CurrentDate)),2) AS FYearName,
		LEFT(DATENAME(MM, @CurrentDate), 3) + '-' + CONVERT(VARCHAR, 
		DATEPART(YY, @CurrentDate)) AS MonthYear,
		RIGHT('0' + CONVERT(VARCHAR, DATEPART(MM, @CurrentDate)),2) +
		CONVERT(VARCHAR, DATEPART(YY, @CurrentDate)) AS MMYYYY,
		CONVERT(DATETIME, CONVERT(DATE, DATEADD(DD, - (DATEPART(DD, 
		@CurrentDate) - 1), @CurrentDate))) AS FirstDayOfMonth,
		CONVERT(DATETIME, CONVERT(DATE, DATEADD(DD, - (DATEPART(DD, 
		(DATEADD(MM, 1, @CurrentDate)))), DATEADD(MM, 1, 
		@CurrentDate)))) AS LastDayOfMonth,
		DATEADD(QQ, DATEDIFF(QQ, 0, @CurrentDate), 0) AS FirstDayOfQuarter,
		DATEADD(QQ, DATEDIFF(QQ, -1, @CurrentDate), -1) AS LastDayOfQuarter,
		CONVERT(DATETIME, '01/01/' + CONVERT(VARCHAR, DATEPART(YY, 
		@CurrentDate))) AS FirstDayOfYear,
		CONVERT(DATETIME, '12/31/' + CONVERT(VARCHAR, DATEPART(YY, 
		@CurrentDate))) AS LastDayOfYear,
		CASE DATEPART(DW, @CurrentDate)
			WHEN 1 THEN 0
			WHEN 2 THEN 1
			WHEN 3 THEN 1
			WHEN 4 THEN 1
			WHEN 5 THEN 1
			WHEN 6 THEN 1
			WHEN 7 THEN 0
			END AS IsWeekday,
		CASE DATEPART(DW, @CurrentDate)
			WHEN 1 THEN 'Weekend'
			WHEN 2 THEN 'Weekday'
			WHEN 3 THEN 'Weekday'
			WHEN 4 THEN 'Weekday'
			WHEN 5 THEN 'Weekday'
			WHEN 6 THEN 'Weekday'
			WHEN 7 THEN 'Weekend'
			END AS IsWeekdayName,
		NULL AS IsHoliday,
		NULL AS IsHolidayName,
		NULL AS Holiday, 
			CASE
			WHEN DATEPART(MM, @CurrentDate) IN (12,1,2) THEN 2
			WHEN DATEPART(MM, @CurrentDate) IN (3,4,5) THEN 3
			WHEN DATEPART(MM, @CurrentDate) IN (6,7,8) THEN 4
			WHEN DATEPART(MM, @CurrentDate) IN (9,10,11) THEN 1
			END AS Season,
		    CASE
			WHEN DATEPART(MM, @CurrentDate) IN (12,1,2) THEN 'Winter'
			WHEN DATEPART(MM, @CurrentDate) IN (3,4,5) THEN 'Spring'
			WHEN DATEPART(MM, @CurrentDate) IN (6,7,8) THEN 'Summer'
			WHEN DATEPART(MM, @CurrentDate) IN (9,10,11) THEN 'Fall'
			END AS SeasonName

	SET @CurrentDate = DATEADD(DD, 1, @CurrentDate)
END


--Update Values of Holiday as per USA Govt. Declaration for National Holiday.

/*Update HOLIDAY Field of USA In dimension*/
	
 	/*THANKSGIVING - Fourth THURSDAY in November*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Thanksgiving Day'
	WHERE
		[Month] = 11 
		AND [DayName] = 'Thursday' 
		AND DayOfWeekInMonth = 4

	/*CHRISTMAS*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Christmas Day'
		
	WHERE [Month] = 12 AND [DayOfMonth]  = 25

	/*4th of July*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Independance Day'
	WHERE [Month] = 7 AND [DayOfMonth] = 4

	/*New Years Day*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'New Year''s Day'
	WHERE [Month] = 1 AND [DayOfMonth] = 1

	/*Memorial Day - Last Monday in May*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Memorial Day'
	FROM [dbo].[DimDate]
	WHERE Date_SK IN 
		(
		SELECT
			MAX(Date_SK)
		FROM [dbo].[DimDate]
		WHERE
			[MonthName] = 'May'
			AND [DayName]  = 'Monday'
		GROUP BY
			[Year],
			[Month]
		)

	/*Labor Day - First Monday in September*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Labor Day'
	FROM [dbo].[DimDate]
	WHERE Date_SK IN 
		(
		SELECT
			MIN(Date_SK)
		FROM [dbo].[DimDate]
		WHERE
			[MonthName] = 'September'
			AND [DayName] = 'Monday'
		GROUP BY
			[Year],
			[Month]
		)

	/*Valentine's Day*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Valentine''s Day'
	WHERE
		[Month] = 2 
		AND [DayOfMonth] = 14

	/*Saint Patrick's Day*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Saint Patrick''s Day'
	WHERE
		[Month] = 3
		AND [DayOfMonth] = 17

	/*Martin Luthor King Day - Third Monday in January starting in 1983*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Martin Luthor King Jr Day'
	WHERE
		[Month] = 1
		AND [DayName]  = 'Monday'
		AND [Year] >= 1983
		AND DayOfWeekInMonth = 3

	/*President's Day - Third Monday in February*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'President''s Day'
	WHERE
		[Month] = 2
		AND [DayName] = 'Monday'
		AND DayOfWeekInMonth = 3

	/*Mother's Day - Second Sunday of May*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Mother''s Day'
	WHERE
		[Month] = 5
		AND [DayName] = 'Sunday'
		AND DayOfWeekInMonth = 2

	/*Father's Day - Third Sunday of June*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Father''s Day'
	WHERE
		[Month] = 6
		AND [DayName] = 'Sunday'
		AND DayOfWeekInMonth = 3

	/*Halloween 10/31*/
	UPDATE [dbo].[DimDate]
		SET Holiday = 'Halloween'
	WHERE
		[Month] = 10
		AND [DayOfMonth] = 31

	/*Election Day - The first Tuesday after the first Monday in November*/
	BEGIN
	DECLARE @Holidays TABLE (ID INT IDENTITY(1,1), 
	DateID int, Week TINYINT, YEAR CHAR(4), DAY CHAR(2))

		INSERT INTO @Holidays(DateID, [Year],[Day])
		SELECT
			Date_SK,
			[Year],
			[DayOfMonth] 
		FROM [dbo].[DimDate]
		WHERE
			[Month] = 11
			AND [DayName] = 'Monday'
		ORDER BY
			YEAR,
			DayOfMonth 

		DECLARE @CNTR INT, @POS INT, @STARTYEAR INT, @ENDYEAR INT, @MINDAY INT

		SELECT
			@CURRENTYEAR = MIN([Year])
			, @STARTYEAR = MIN([Year])
			, @ENDYEAR = MAX([Year])
		FROM @Holidays

		WHILE @CURRENTYEAR <= @ENDYEAR
		BEGIN
			SELECT @CNTR = COUNT([Year])
			FROM @Holidays
			WHERE [Year] = @CURRENTYEAR

			SET @POS = 1

			WHILE @POS <= @CNTR
			BEGIN
				SELECT @MINDAY = MIN(DAY)
				FROM @Holidays
				WHERE
					[Year] = @CURRENTYEAR
					AND [Week] IS NULL

				UPDATE @Holidays
					SET [Week] = @POS
				WHERE
					[Year] = @CURRENTYEAR
					AND [Day] = @MINDAY

				SELECT @POS = @POS + 1
			END

			SELECT @CURRENTYEAR = @CURRENTYEAR + 1
		END

		UPDATE [dbo].[DimDate]
			SET Holiday  = 'Election Day'				
		FROM [dbo].[DimDate] DT
			JOIN @Holidays HL ON (HL.DateID + 1) = DT.Date_SK
		WHERE
			[Week] = 1
	END
	--set flag for USA holidays in Dimension
	UPDATE [dbo].[DimDate]

SET IsHoliday = CASE WHEN Holiday  IS NULL THEN 0 
						WHEN Holiday  IS NOT NULL THEN 1 END

	UPDATE [dbo].[DimDate]

SET IsHolidayName = CASE WHEN Holiday  IS NULL THEN 'Not a holiday' 
						WHEN Holiday  IS NOT NULL THEN 'Holiday' END
```

### DimItem
```sql
SELECT
    ItemID AS Item_BK,
    Item,
    Color,
    Brand
FROM
    SilhouetteCollective.dbo.Item i
LEFT JOIN
    SilhouetteCollective.dbo.Color c ON i.ColorID = c.ColorID
LEFT JOIN
    SilhouetteCollective.dbo.Brand b ON i.BrandID = b.BrandID;
```

### DimCustomer
```sql
SELECT
	CustomerID AS Customer_BK,
	LastName,
	FirstName,
	CONCAT(LastName, N', ', FirstName) AS LFName,
	CONCAT(FirstName, N' ', LastName) AS FLName,
	ISNULL(City, N'Unknown') AS City,
	ISNULL(StateName, N'Unknown') AS [State],
	ISNULL(RegionName, N'Unknown') AS Region,
	CASE Gender
	WHEN 'M' THEN N'Male'
	WHEN 'F' THEN N'Female'
	WHEN 'N' THEN N'Non-binary'
	ELSE N'Unknown'
	END AS Gender,
	CASE 
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) < 18 THEN N'Under 18'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 18 AND 24 THEN N'18-24'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 25 AND 34 THEN N'25-34'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 35 AND 44 THEN N'35-44'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 45 AND 54 THEN N'45-54'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 55 AND 64 THEN N'55-64'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) >= 65 THEN N'65 and older'
	ELSE N'Unknown'
	END AS AgeGroup,
	CASE 
	WHEN YEAR(Birthdate) BETWEEN 1901 AND 1927 THEN N'Greatest Generation'
	WHEN YEAR(Birthdate) BETWEEN 1928 AND 1945 THEN N'Silent Genearation'
	WHEN YEAR(Birthdate) BETWEEN 1946 AND 1964 THEN N'Baby Boomer'
	WHEN YEAR(Birthdate) BETWEEN 1965 AND 1979 THEN N'Gen X'
	WHEN YEAR(Birthdate) BETWEEN 1980 AND 1996 THEN N'Millenial'
	WHEN YEAR(Birthdate) BETWEEN 1997 AND 2012 THEN N'Gen Z'
	WHEN YEAR(Birthdate) BETWEEN 2013 AND 2025 THEN N'Gen Alpha'
	ELSE N'Unknown'
	END AS Generation
FROM
	SilhouetteCollective.dbo.Customer c
LEFT JOIN
	SilhouetteCollective.dbo.[State] st
ON
	c.StateCode = st.StateCode
LEFT JOIN
	SilhouetteCollective.dbo.Region r
ON
	st.RegionCode = r.RegionCode;

### DimEventType
```sql
SELECT
	EventTypeID AS EventType_BK,
	EventType
FROM
	SilhouetteCollective.dbo.EventType;
```
### DimShopper
```sql
SELECT
	ShopperID AS Shopper_BK,
	LastName,
	FirstName,
	CONCAT(LastName, N', ', FirstName) AS LFName,
	CONCAT(FirstName, N' ', LastName) AS FLName,
	ISNULL(City, N'Unknown') AS City,
	ISNULL(StateName, N'Unknown') AS [State],
	ISNULL(RegionName, N'Unknown') AS Region,
	CASE Gender
	WHEN 'M' THEN N'Male'
	WHEN 'F' THEN N'Female'
	WHEN 'N' THEN N'Non-binary'
	ELSE N'Unknown'
	END AS Gender,
	CASE 
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) < 18 THEN N'Under 18'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 18 AND 24 THEN N'18-24'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 25 AND 34 THEN N'25-34'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 35 AND 44 THEN N'35-44'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 45 AND 54 THEN N'45-54'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) BETWEEN 55 AND 64 THEN N'55-64'
	WHEN DATEDIFF(YY, Birthdate, GETDATE()) >= 65 THEN N'65 and older'
	END AS AgeGroup,
	CASE 
	WHEN YEAR(Birthdate) BETWEEN 1901 AND 1927 THEN N'Greatest Generation'
	WHEN YEAR(Birthdate) BETWEEN 1928 AND 1945 THEN N'Silent Genearation'
	WHEN YEAR(Birthdate) BETWEEN 1946 AND 1964 THEN N'Baby Boomer'
	WHEN YEAR(Birthdate) BETWEEN 1965 AND 1979 THEN N'Gen X'
	WHEN YEAR(Birthdate) BETWEEN 1980 AND 1996 THEN N'Millenial'
	WHEN YEAR(Birthdate) BETWEEN 1997 AND 2012 THEN N'Gen Z'
	WHEN YEAR(Birthdate) BETWEEN 2013 AND 2025 THEN N'Gen Alpha'
	END AS Generation
FROM
	SilhouetteCollective.dbo.Shopper s
LEFT JOIN
	SilhouetteCollective.dbo.[State] st
ON
	s.StateCode = st.StateCode
LEFT JOIN
	SilhouetteCollective.dbo.Region r
ON
	st.RegionCode = r.RegionCode;
```
### FactPurchase
```sql
SELECT
	p.PurchaseID,
	pri.PurchaseItemID,
	dimd.Date_SK AS PurchaseDate,
	dimc.Customer_SK,
	dims.Shopper_SK,
	dimi.Item_SK,
	dime.EventType_SK,
	i.Price AS ItemPrice,
	i.Cost AS ItemCost,
	i.Price - i.Cost AS ItemProfit,
	pri.Quantity,
	i.Price * pri.Quantity AS Revenue,
	i.Cost * pri.Quantity AS Cost,
	(i.Price * pri.Quantity) - i.Cost * pri.Quantity AS Profit
FROM
	SilhouetteCollective.dbo.PurchaseItem pri
LEFT JOIN
	SilhouetteCollective.dbo.Purchase p
ON
	pri.PurchaseID = p.PurchaseID
LEFT JOIN	
	SilhouetteCollective.dbo.Item i
ON
	pri.ItemID = i.ItemID
LEFT JOIN
	SilhouetteCollectiveDM.dbo.DimCustomer dimc
ON
	dimc.Customer_BK = p.CustomerID
LEFT JOIN
	SilhouetteCollectiveDM.dbo.DimShopper dims
ON
	dims.Shopper_BK = p.ShopperID
LEFT JOIN
	SilhouetteCollectiveDM.dbo.DimItem dimi
ON
	dimi.Item_BK = pri.ItemID
LEFT JOIN
	SilhouetteCollectiveDM.dbo.DimEventType dime
ON
	dime.EventType_BK = p.EventTypeID
LEFT JOIN
	SilhouetteCollectiveDM.dbo.DimDate dimd
ON
	dimd.[Date] = p.PurchaseDate;
```
[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)
	
<a name="PowerBI"></a>
<hr>
	
## Sales Dashboard in Power BI

### Dashboard
![image](https://github.com/user-attachments/assets/ad429715-cf50-42ed-a519-4a55147fcf19)

### Analysis

#### Key Findings

1. **Top and Bottom States by Revenue:**
   - The top three states generating the most revenue are California ($322,570), Texas ($319,175), and Florida ($223,820).
   - The bottom three states are Rhode Island ($4,345), Maine ($1,750), and Vermont ($1,615).
   - The top states have larger populations, while the bottom states are concentrated on the East Coast.

2. **Profit by Year:**
   - The **Profit by Year** line chart reveals a significant effect of the **Covid-19 pandemic** on profits, especially in 2020.
   - **March to April 2020** shows a dramatic increase in profit as customers were confined to their homes.
   - **May 2020** shows a drop in profit as customer income slowed due to job losses, with fewer people willing to spend during uncertain times.
   - There is consistent low profit from **January to March** each year, and higher profits around **Halloween**, **Thanksgiving**, and **Christmas**. 
   - A consistent drop in profit is observed from **August to September** each year.

3. **Event Type Revenue and Profit:**
   - **Club** category: Revenue around **$147,600**, with costs of **$90,000**, leading to a profit of **$57,010**.
   - **Night-General** category: Revenue around **$1,000,000**, with costs of **$610,000**, resulting in a profit of **$389,225**.

4. **Item Orders:**
   - **Hats** are the number one item being bought, with the other two items trailing closely behind.
   - As a smaller company, we started with a limited item selection to test market success before expanding.

---

### Recommendations

1. **Invest More on the East Coast:**
   - Increase marketing efforts in east coast states by gathering customer contact information (e.g., email, text message sign-ups) for targeted campaigns.
   - Conduct annual surveys asking customers what products they want to see, considering regional preferences (e.g., winter items in colder climates).

2. **Address the Profit Drop from August to September:**
   - Implement special deals during these months to boost profit and incentivize customers to begin holiday shopping earlier.
   - Create **fall deals** as clothing companies start transitioning into winter clothing, aligning with seasonal demands.
   - Expand the product offerings to include **more summer clothing** to increase profits at the end of summer/beginning of fall.

3. **Tailor Product Offerings Based on Event Types:**
   - Focus on expanding products for high-revenue Event Types like **Night-General** and **Wedding**.
   - Limit product offerings for low-revenue categories like **Club** and **Day-General**, potentially reducing costs by introducing more affordable products.

4. **Expand Item Selection:**
   - Use customer survey results to identify what products consumers want, and tailor product offerings based on these findings.
   - Regularly assess which items perform best and which need to be adjusted or phased out, ensuring alignment with consumer demands nationwide.

[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)

