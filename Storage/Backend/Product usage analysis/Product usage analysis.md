---
created: 2024-05-24T21:38
updated: 2026-01-31T13:32
---

Welcome to my Product Usage Analysis, the purpose of this analysis is to guide me towards more intentional buying, particularly in finding products that strike a good balance between price and durability. The ultimate goal is to reach a cost per use as near as possible to $0.00, indicating maximum value derived from the product.

It's a tool I use to make more informed decisions about future purchases, and I hope it can provide some insights for you as well.

>This project was inspired by [Steph Ango](https://stephango.com/about), particularly by his [Buy Wisely](https://stephango.com/buy-wisely) post.

<!-- QueryToSerialize: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",  product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->
<!-- SerializedQuery: table without id name as Product, "$" + round(price/(monthly-uses*((date(today) - acquired).months)),2) as "Cost per use", monthly-uses as "Uses per month", dateformat(acquired, "yyyy-MM") as Acquired, round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(today) - acquired).months),0) as "Total uses",  product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/(monthly-uses*((date(today) - acquired).months)),2) asc -->

| Product                | Cost per use | Uses per month | Acquired | Months | Price | Total uses | Product category |
| ---------------------- | ------------ | -------------- | -------- | ------ | ----- | ---------- | ---------------- |
| Braun Alarm            | $0.01        | 30             | 2022-02  | 40.1   | $15   | 1202       | Alarm            |
| Bottle Bottle          | $0.1         | 20             | 2024-05  | 12.5   | $24   | 250        | Water Bottle     |
| Xiaomi Mi Hybrid       | $0.1         | 20             | 2024-01  | 17.1   | $34   | 342        | Audio            |
| Moser Hair Trimmer     | $0.11        | 8              | 2022-04  | 38.1   | $35   | 305        | Hair Trimmer     |
| Bellroy Tokyo Totepack | $0.2         | 25             | 2022-10  | 31.4   | $160  | 785        | Backpack         |
| inCharge XL            | $0.34        | 5              | 2023-10  | 19.8   | $34   | 99         | Charging Cable   |
| AirUp                  | $0.57        | 5              | 2023-05  | 24.6   | $70   | 123        | Water Bottle     |
| Ipod 5th               | $0.88        | 10             | 2024-01  | 17.1   | $150  | 171        | Audio            |
| MacBook M1             | $1.07        | 28             | 2022-10  | 31.7   | $950  | 887        | PC               |
<!-- SerializedQuery END -->

>**For analysis of rarely used products, see [[Rarely Used Products Analysis]].**

##### Discontinued Products 🪦

This paragraph is dedicated to the products that have served their purpose and are no longer in use. They might be discontinued, replaced, or simply outlived their usefulness. But their departure doesn't diminish their value. Each product listed here was good in its own right and served its purpose well during its tenure. 

So, let's take a moment to appreciate these products and analyze their usage cost over the time they were with us.

<!-- QueryToSerialize: table without id name as Product, "$" + round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) as "Cost per use", dateformat(acquired, "yyyy-MM") as Acquired, dateformat(discontinued, "yyyy-MM") as "Discontinued", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(discontinued) - acquired).months),0) as "Total uses", product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued != null and date(discontinued) <= date(today)) sort round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) asc -->
<!-- SerializedQuery: table without id name as Product, "$" + round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) as "Cost per use", dateformat(acquired, "yyyy-MM") as Acquired, dateformat(discontinued, "yyyy-MM") as "Discontinued", "$" + string(round(price, 2)) as Price, round(monthly-uses*((date(discontinued) - acquired).months),0) as "Total uses", product-category as "Product category" where monthly-uses > 0 and contains(type, [[Product usage analysis]]) and (discontinued != null and date(discontinued) <= date(today)) sort round(price/(monthly-uses*((date(discontinued) - acquired).months)),2) asc -->

| Product | Cost per use | Acquired | Discontinued | Price | Total uses | Product category |
| ------- | ------------ | -------- | ------------ | ----- | ---------- | ---------------- |
| test    | $0.13        | 2024-02  | 2024-10      | $1    | 8          | Alarm            |
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
