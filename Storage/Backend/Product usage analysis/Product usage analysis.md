
<!-- QueryToSerialize: table rating as Rating, "$" + round(price/(monthly-uses*((date(today) -acquired).months)),2) as "Per use", monthly-uses as "Uses/month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses", type as Type where monthly-uses > 0 and contains(category, [[Product usage analysis]]) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
<!-- SerializedQuery: table rating as Rating, "$" + round(price/(monthly-uses*((date(today) -acquired).months)),2) as "Per use", monthly-uses as "Uses/month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses", type as Type where monthly-uses > 0 and contains(category, [[Product usage analysis]]) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
| File                                                                                           | Rating | Per use | Uses/month | Acquired | Months | Price | Total uses | Type           |
| ---------------------------------------------------------------------------------------------- | ------ | ------- | ---------- | -------- | ------ | ----- | ---------- | -------------- |
| [[Storage/Backend/Product usage analysis/Braun Alarm (product).md\|Braun Alarm (product)]]     | -      | $0.02   | 30         | 2022-02  | 27.6   | $15   | 828        | Alarm          |
| [[Storage/Backend/Product usage analysis/Moser Hair Trimmer.md\|Moser Hair Trimmer]]           | -      | $0.17   | 8          | 2022-04  | 25.8   | $35   | 206        | Hair Trimmer   |
| [[Storage/Backend/Product usage analysis/Tokyo Totepack.md\|Tokyo Totepack]]                   | -      | $0.33   | 25         | 2022-10  | 19.2   | $160  | 479        | Backpack       |
| [[Storage/Backend/Product usage analysis/inCharge XL (product).md\|inCharge XL (product)]]     | -      | $0.93   | 5          | 2023-10  | 7.3    | $34   | 36         | Charging Cable |
| [[Storage/Backend/Product usage analysis/AirUp (product).md\|AirUp (product)]]                 | -      | $1.15   | 5          | 2023-05  | 12.2   | $70   | 61         | Water Bottle   |
| [[Storage/Backend/Product usage analysis/Bottle Bottle (product).md\|Bottle Bottle (product)]] | -      | $36     | 20         | 2024-05  | 0      | $24   | 1          | Water Bottle   |
<!-- SerializedQuery END -->


```dataview
table 
	rating as Rating,
	"$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Per use",
	monthly-uses as "Uses/month",
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
