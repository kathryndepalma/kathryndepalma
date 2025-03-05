<a name="top"></a>

[<img src="https://user-images.githubusercontent.com/91146906/152112781-2de05074-70b1-436b-9bfb-860890cc1de1.svg" height="35"/>](../#OLAP)
<hr>

# Silhouette Collective: A Fashion Concierge Business
[<img src="https://user-images.githubusercontent.com/91146906/152239160-8f8c18a2-e724-4be7-863d-bc94151212ce.svg" height="35"/>](#Introduction)
[<img src="https://user-images.githubusercontent.com/91146906/152279618-21ae078d-3d0b-45ed-95f1-306e5030f301.svg" height="35"/>](#BusinessRequirements)
[<img src="https://user-images.githubusercontent.com/91146906/152279677-02eb9847-1863-4641-b59c-58a0e6cd2f24.svg" height="35"/>](#DataMartDesign)
[<img src="https://user-images.githubusercontent.com/91146906/161397633-2e4d30dc-ba35-4fe9-b66d-9c8e91ba0f86.svg" height="35"/>](#PowerPivot)
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
    <th>Brand</th>
    <th>Item</th>
    <th>Customer</th>
    <th>Special</th>
  </tr>
  <tr>
    <td>Year</td>
    <td>ShopperID</td>
    <td>BrandID</td>
    <td>ItemID</td>
    <td>CustomerID</td>
    <td>SpecialRequestID</td>
  </tr>
  <tr>
    <td>Quarter</td>
    <td>Shopper Name</td>
    <td>BrandName</td>
    <td>ItemName</td>
    <td>CustomerName</td>
    <td>CustomerID</td>
  </tr>
  <tr>
    <td>Month</td>
    <td></td>
    <td>BrandRank</td>
    <td>Color</td>
    <td>Size</td>
    <td>Event</td>
  </tr>
  <tr>
    <td>Date</td>
    <td></td>
    <td></td>
    <td>BrandName</td>
    <td>MainColorPref</td>
    <td>BrandName</td>
  </tr>
  <tr>
    <td></td>
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
DimDate is loaded using the LoadDimDate.sql SQL query, which was provided.
<br>
<br>[<img src="https://user-images.githubusercontent.com/91146906/152286999-322b92ed-de1a-46f6-a8ff-9bc08b12f9ca.svg" height="35"/>](..Portfolio/SilhouetteCollective/CollectiveLoadDimDate.sql)

### DimItem
SELECT
	ItemID AS Item_BK,
	Item,
	Color,
	Brand
FROM
	SilhouetteCollective.dbo.Item i
LEFT JOIN
	SilhouetteCollective.dbo.Color c
ON
	i.ColorID = c.ColorID
LEFT JOIN
	SilhouetteCollective.dbo.Brand b
ON
	i.BrandID = b.BrandID;

### DimCustomer
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
SELECT
	EventTypeID AS EventType_BK,
	EventType
FROM
	SilhouetteCollective.dbo.EventType;

### DimShopper
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

### FactPurchase
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

[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)
	
<a name="PowerPivot"></a>
<hr>
	
## Sales Analysis in Tableau

### Dashboard
	
![BackToRootsDMPowerPivotSnapshot](https://user-images.githubusercontent.com/91146906/152288743-11ae6130-9ac9-4bc7-b06e-bed1f1f68ab7.png)
	
### Analysis
The "Sales Overtime by Product Type" indicate special orders have the most sales for Back to Roots by a significant margin. In January 2020, special orders had their peak sales of $617,620. Cookies have more sales around the holiday season and winter (December through February), with their peak sales of $249,363.50 in January 2020. The sales of other product types do not significantly differ from one another.
<br>
<br>The "Sales Overtime by Product Type" also demonstrate an upward trend in sales until the COVID-19 pandemic hit, at which point sales dropped significantly as the bakery had to close for several months. Upon reopening, sales began to increase again, although they have not reached pre-pandemic levels. The "Number of Orders by Order Fulfillment Method" also demonstrates the impact of the COVID-19 pandemic. Prior to the pandemic, in-store order fulfillment was used for 21,733 orders in Q1 2020, compared to 14,437 that used pick-up and 5,833 that used delivery. During Q2 2020, orders were only filled via delivery, as it was the heart of the COVID-19 pandemic. As the community began to adapt to life amid COVID-19, the number of orders using pick-up surpassed those using delivery; however, in-store order fulfilments remain low. There were 6,299 orders filled via pick-up in Q4 2020, while 5,539 were filled via delivery and 2,131 via in-store. With the "Number of Orders by Order Fulfillment Method" analysis, the data suggests in-store order fulfillment methods are declining, while pick-up and delivery methods are increasing.
<br>
<br>The "Quantity Sold by Product" analysis indicates Raspberry Thumbprint Cookies have the highest quantity sold over all time and are particularly popular in the winter, as are many cookies. Conversely, crisps have a low quantity sold and are not sold in the winter. The pumpkin products, naturally, have the most unit sales in the fall. The data in this analysis suggests some products are highly season, like Gingerbread Truffles, while others are not, like Special Order Cakes. Further, this analysis in relation to the sales analysis, suggests that both cookies and special orders have high sales and quantity sold; however, a much higher quantity of cookies are sold without matching the sales brought in by special orders due to the significant price difference. Balls also have a high quantity of sales, although that does not necessarily seem to show in the sales analysis.
<br>
<br>The "Sales by Diet Type" analysis indicates the "Unknown" diet has the highest sales, which may be explained by these products being special order and meeting whatever dietary requirements are requested. Gluten-free, honey-free, nut-free, processed sugar-free, and vegan products consistently have the highest sales of products with known diet types, while those without nuts are slightly lower and those also without honey are the lowest. However, it cannot be determined with this analysis whether the difference in sales is due to the product's diet types or other factors, like the products themselves and the number of products meeting each diet type available. 
	
### Recommendations 
<ul>
  <li>Back to Roots should promote and invest in special orders, as this is where Back to Roots has the most sales.</li>
  <li>Since "balls" have a high quantity of sales that does not reflect in the dollar value of sales, it may be worthwhile to further investigate this and determine how the popularity of the "ball" product types can translate to a higher dollar value of sales. Can prices be increased?</li>
  <li>Back to Roots should track demand for order fulfillment methods as the community continues to recover from the pandemic. If the current trend continues, Back to Roots should focus more on developing delivery and pick-up processes, rather than in-store fulfillment.</li>
  <li>Seasonal products are popular, and Back to Roots should take advantage of that by following seasonal trends and using seasonal ingredients.</li>
  <li>Back to Roots may consider evaluating consumers' diet preferences and adapt their products to meet those, as this may lead to a better understanding of how diet impacts sales.</li>
</ul>

[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)
	
<a name="PowerBI"></a>
<hr>
	
## Customer and Order Dashboard (Power BI)
### Chief Marketing Officer's Question
What are the sales monthly, quarterly, and yearly summarized by customer age and reward status, in addition to order placement method?

### Dashboard
<img width="1211" alt="BackToRootsDashboard" src="https://user-images.githubusercontent.com/91146906/152289272-89e5505c-4e6a-4f29-b516-66ec308c28af.png">

### Analysis
Sales experienced a steady increase, despite seasonality, from Back-to-Root's opening in February 2018 through September 2019, then a sharp increase was seen in October 2019. Sales hit their peak of $1,273,807.50 in January 2020 before a drastic drop to $147,357 in April 2020 due to the COVID-19 pandemic and the associated impacts. Back-to-Roots closed for a period and then was only able to offer delivery and pick-up options. Since then, sales have once again been steadily increasing and are projected to continue doing so, although seasonality will result in some increases and decreases in sales.
<br>
<br>Of the Back-to-Roots customers who have disclosed birthdays, most (574) customers fall in the 30-39 age group and make-up $1.32 million of the $17.51 million sales. The data suggests these customers prefer an online order placement method, with 43.9% of orders by customers aged 30-39 placed online (compared to 33.9% for all customers). Similarly, the 490 customers aged 40-49, 446 customers aged 20-29, and 362 customers aged 50-59 place more orders online than in-store or via phone. While all age groups place a percentage of orders in-store, this order placement method is used most often by customers with undisclosed birthdays. This could be because it is easy to input your birthday when placing an online order, and it is less common to disclose birthday information when in-store.
<br>
<br>Of the orders associated with a rewards status (i.e. not placed by customers with no rewards), 45.3% are placed online (compared to 33.9% for all orders) and 39.1% are placed in-store (compared to 51.4% for all orders). Thus, the data suggests that more loyal customers prefer the online order placement method. Further, orders not associated to a reward status have an average order total of $85, while orders associated to the bronze status average $95, associated to silver status average $96, associated to gold status average $93, and associated to platinum status average $94. Thus, the data suggests having a reward status leads to more spending per order, but the level of reward status does not necessarily make a difference.
<br>
<br>The majority of sales are from customers with Boulder and Longmont addresses, likely because there are Back-to-Roots locations in each of these places. There are also some sales from customers in Niwot and Lafayette; however, sales are isolated to customers in these four cities.

### Recommendations
<ul>
  <li>Continue developing, improving, and promoting the online order placement system, as many loyal customers prefer this order placement method.</li>
  <li>Promote rewards program, as it may lead to more spending per order. Further, consider adjusting incentives between rewards tiers to increase spending.</li>
  <li>Market to potential customers in cities surrounding Boulder, Longmont, Niwot, and Lafayette to increase customer base (delivery may be appealing).</li>
</ul>

[<img src="https://user-images.githubusercontent.com/91146906/152072378-b0168a2d-e85c-47c6-a272-fcfb3f6a44ae.svg" height="35"/>](#top)

