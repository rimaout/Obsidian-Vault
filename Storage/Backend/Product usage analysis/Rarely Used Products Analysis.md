---
created: 2024-05-31T18:30
updated: 2026-01-31T13:32
---
Welcome to the analysis of not frequently used products. Here, we track the cost per use of these items, updating the usage count manually each time a product is used. This approach provides a more accurate reflection of the cost for these rarely used products.

>**Head back to the main page for more, including the analysis of frequently used products: [[Product usage analysis]]**
##### Products Still in Use

<!-- QueryToSerialize: table without id name as "Product", "$" + round(price/uses,2) as "Cost per use", dateformat(acquired, "yyyy-MM") as "Acquired", round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as "Price", uses as "Total uses", product-category as "Category" where uses > 0 and contains(type, [[Rarely Used Products Analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/uses,2) asc -->
<!-- SerializedQuery: table without id name as "Product", "$" + round(price/uses,2) as "Cost per use", dateformat(acquired, "yyyy-MM") as "Acquired", round((date(today) - acquired).months,1) as "Months", "$" + string(round(price, 2)) as "Price", uses as "Total uses", product-category as "Category" where uses > 0 and contains(type, [[Rarely Used Products Analysis]]) and (discontinued = null or date(discontinued) > date(today)) sort round(price/uses,2) asc -->

| Product | Cost per use | Acquired | Months | Price | Total uses | Category |
| ------- | ------------ | -------- | ------ | ----- | ---------- | -------- |
<!-- SerializedQuery END -->

### How this works

Instead of calculating their cost per use automatically each month (as I do for [[Product usage analysis]]), I manually increase a `uses` counter each time I use the product. This provides a more accurate cost per use calculation for these rarely used items.

```dataview
table without id
    name as "Product",
    "$" + round(price/uses,2) as "Cost per use",
    dateformat(acquired, "yyyy-MM") as "Acquired",
    round((date(today) - acquired).months,1) as "Months",
    "$" + string(round(price, 2)) as "Price",
    uses as "Total uses",
    product-category as "Category"
where
    uses > 0 and
    contains(type, [[Rarely Used Products Analysis]]) and (discontinued = null or date(discontinued) > date(today))
sort
    round(price/uses,2) asc
```

```dataview
table without id
    name as "Product",
    "$" + round(price/uses,2) as "Cost per use",
    dateformat(acquired, "yyyy-MM") as "Acquired",
    dateformat(discontinued, "yyyy-MM") as "Discontinued",
    round((date(discontinued) - acquired).months,1) as "Months",
    "$" + string(round(price, 2)) as "Price",
    uses as "Total uses",
    product-category as "Category"
where
    uses > 0 and
    contains(type, [[Rarely Used Products Analysis]]) and (discontinued != null and date(discontinued) <= date(today))
sort
    round(price/uses,2) asc
```

