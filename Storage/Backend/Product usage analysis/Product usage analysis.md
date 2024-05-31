---
created: 2024-05-24T21:38
updated: 2024-05-31T21:38
---

Welcome to my Product Usage Analysis, the purpose of this analysis is to guide me towards more intentional buying, particularly in finding products that strike a good balance between price and durability. The ultimate goal is to reach a cost per use of $0.00, indicating maximum value derived from the product.

It's a tool I use to make more informed decisions about future purchases, and I hope it can provide some insights for you as well.

This project was inspired by [Steph Ango](https://stephango.com/about), particularly by his [Buy Wisely](https://stephango.com/buy-wisely) post.

<!-- QueryToSerialize: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",  product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
<!-- SerializedQuery: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",  product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
| Product            | Cost per use | Uses per month | Acquired | Months | Price | Total uses | Product category |
| ------------------ | ------------ | -------------- | -------- | ------ | ----- | ---------- | ---------------- |
| Braun Alarm        | $0.02        | 30             | 2022-02  | 27.8   | $15   | 835        | Alarm            |
| Moser Hair Trimmer | $0.17        | 8              | 2022-04  | 25.9   | $35   | 208        | Hair Trimmer     |
| Xiaomi Mi Hybrid   | $0.34        | 20             | 2024-01  | 5      | $34   | 99         | Audio            |
| inCharge XL        | $0.91        | 5              | 2023-10  | 7.5    | $34   | 38         | Charging Cable   |
| AirUp              | $1.13        | 5              | 2023-05  | 12.4   | $70   | 62         | Water Bottle     |
| Bottle Bottle      | $4.8         | 20             | 2024-05  | 0.3    | $24   | 5          | Water Bottle     |
<!-- SerializedQuery END -->

>**For analysis of rarely used products, see [Rarely Used Products Analysis](path/to/rarely-used-products.md).**

##### Discontinued Products 🪦
This paragraph is dedicated to the products that have served their purpose and are no longer in use. They might be discontinued, replaced, or simply outlived their usefulness. But their departure doesn't diminish their value. Each product listed here was good in its own right and served its purpose well during its tenure. 

So, let's take a moment to appreciate these products and analyse their usage cost over the time they were with us.

<!-- QueryToSerialize: table without id name as Product, "$" + round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) as "Cost per use", dateformat(acquired, "yyyy-MM") as Acquired, dateformat(discontinued, "yyyy-MM") as "Discontinued", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(discontinued) - acquired).months),0) as "Total uses", product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued != null and date(discontinued) <= date(today)) sort round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) asc -->
<!-- SerializedQuery: table without id name as Product, "$" + round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) as "Cost per use", dateformat(acquired, "yyyy-MM") as Acquired, dateformat(discontinued, "yyyy-MM") as "Discontinued", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(discontinued) - acquired).months),0) as "Total uses", product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued != null and date(discontinued) <= date(today)) sort round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) asc -->
| Product                | Cost per use | Acquired | Discontinued | Price | Total uses | Product category |
| ---------------------- | ------------ | -------- | ------------ | ----- | ---------- | ---------------- |
| Bellroy Tokyo Totepack | $0.11        | 2019-05  | 2024-05      | $160  | 1509       | Backpack         |
<!-- SerializedQuery END -->

---
### How This Table Works

The table is generated using the [dataview plugin](https://github.com/blacksmithgu/obsidian-dataview), which pulls data from my notes and calculates the cost per use of each product. However, to display this dynamic table on the website, I use another plugin called [dataview serializer](https://github.com/dsebastien/obsidian-dataview-serializer). This plugin creates a static markdown table for the data that can be rendered on the site.

**Dataview tables code:**

```dataview
table without id
    name as "Product",
    "$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use",
    monthly-uses as "Uses per month",
    dateformat(acquired, "yyyy-MM") as "Acquired",
    round((date(today) - acquired).months,1) as "Months",
    "$" + string(round(price, 2)) as "Price",
    round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",
    product-category as "Type"
where
    monthly-uses > 0 and
    contains(type, [[Product usage analysis]]) and (discontinued = null or date(discontinued) > date(today))
sort
    round(price/(monthly-uses*((date(today) - acquired).months)),2) asc
```

```dataview
table without id
    name as Product,
    "$" + round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) as "Cost per use",
    dateformat(acquired, "yyyy-MM") as "Acquired",
    dateformat(discontinued, "yyyy-MM") as "Discontinued",
    round((date(discontinued) - acquired).months,1) as "Months",
    "$" + string(round(price, 2)) as "Price",
    round(monthly-uses*((date(discontinued) - acquired).months),0) as "Total uses",
    product-category as "Type"
where
    monthly-uses > 0 and
    contains(type, [[Product usage analysis]]) and (discontinued != null and date(discontinued) <= date(today))
sort
    round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) asc
```

---
