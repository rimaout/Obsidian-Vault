
Welcome to my Product Usage Analysis, the purpose of this analysis is to guide me towards more intentional buying, particularly in finding products that strike a good balance between price and durability. The ultimate goal is to reach a cost per use of $0.00, indicating maximum value derived from the product.

It's a tool I use to make more informed decisions about future purchases, and I hope it can provide some insights for you as well.

This project was inspired by [Steph Ango](https://stephango.com/about), particularly by his [Buy Wisely](https://stephango.com/buy-wisely) post.

<!-- QueryToSerialize: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) -acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses", type as Type where monthly-uses > 0 and contains(category, [[Product usage analysis]]) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
<!-- SerializedQuery: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) -acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses", type as Type where monthly-uses > 0 and contains(category, [[Product usage analysis]]) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
| Product                | Cost per use | Uses per month | Acquired | Months | Price | Total uses | Type           |
| ---------------------- | ------------ | -------------- | -------- | ------ | ----- | ---------- | -------------- |
| Braun Alarm            | $0.02        | 30             | 2022-02  | 27.6   | $15   | 829        | Alarm          |
| Moser Hair Trimmer     | $0.17        | 8              | 2022-04  | 25.8   | $35   | 206        | Hair Trimmer   |
| Bellroy Tokyo Totepack | $0.33        | 25             | 2022-10  | 19.2   | $160  | 480        | Backpack       |
| Xiaomi Mi Hybrid       | $0.36        | 20             | 2024-01  | 4.8    | $34   | 96         | Audio          |
| inCharge XL            | $0.93        | 5              | 2023-10  | 7.3    | $34   | 37         | Charging Cable |
| AirUp                  | $1.15        | 5              | 2023-05  | 12.2   | $70   | 61         | Water Bottle   |
| Bottle Bottle          | $18          | 20             | 2024-05  | 0.1    | $24   | 1          | Water Bottle   |
<!-- SerializedQuery END -->

---
##### How This Table Works

The table is generated using the [dataview plugin](https://github.com/blacksmithgu/obsidian-dataview), which pulls data from my notes and calculates the cost per use of each product. However, to display this dynamic table on the website, I use another plugin called [dataview serializer](https://github.com/dsebastien/obsidian-dataview-serializer). This plugin creates a static markdown table for the data that can be rendered on the site.

**Here is the code of the dataview table:**

```dataview
table without id
	name as Product,
	"$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use",
	monthly-uses as "Uses per month",
	dateformat(acquired, "yyyy-MM") as Acquired,
	round((date(today) - acquired).months,1) as "Months",
	"$" + string(round(price, 2)) as Price,
	round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",
	type as Type
where
	monthly-uses > 0 and
	contains(category, [[Product usage analysis]])
sort
	round(price/(monthly-uses*((date(today) - acquired).months)),2) asc
```
