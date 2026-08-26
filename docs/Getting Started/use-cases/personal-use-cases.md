---
title: Personal Use Cases
excerpt: Control D is for everyone. Yes, even you.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
{user.LB}

This guide describes the ranking factors used in standard {user.search} ranking configurations.

<Callout icon="📘" theme="info">
  ### Note

  If you're using {user.br} Advanced based ranker (ABR), follow the guide to understand <Anchor target="_blank" href="https://documentation.bloomreach.com/discovery/docs/search-ranking-with-abr">how search ranking works with ABR</Anchor>.
</Callout>

Once a set of products is returned for a search query, {user.br} search intelligence adjusts the order of those products to optimize for higher expected revenue per visit (RPV) for the query. Several factors contribute to the algorithm that optimizes product ranking. A high-level explanation of the various signals is included below.

## Ranking signals

{user.br} calculates several scores for each product to determine the relative rankings:

- Product performance score
- Personalization score
- Relevance score

<Callout icon="🌟" theme="default">
  Performance Score, Personalization Score, and Relevance Score is [powered by](https://www.bloomreach.com/en/products/loomi) {user.lai}
</Callout>

These core ranking scores are adjusted with inventory-based signals such as:

- SKU popularity
- Product Freshness/Recency

{user.br} combines these scores to compute an overall ranking score for each product in the retrieved set of products. The products are sorted in descending order of that score. You can override these ranking scores by setting conditional boost and bury rules in the {user.br} dashboard. This will tweak the order in which products are returned in the results.

<Callout icon="📘" theme="info">
  ### Note

  Category ranking uses all the ranking signals except the [Relevance score](https://documentation.bloomreach.com/discovery/docs/search-ranking#relevance-score). All items in a category have equal relevance.
</Callout>

### Product performance score

{user.br} uses many signals to compute a performance score for each returned product. The primary signal includes a blend of product views, add to carts, conversions and revenue which the products generate for a given search query. For customers that have Product Collections (or variant groups) in their catalog, {user.br} optimizes ranking of both the Collections as well as their component products/SKUs.

- How does {user.br} calculate performance scores?<br />{user.br} uses pixels on the site to capture the raw data that drive performance scores. The signals are refreshed on a daily basis to adjust to changing usage patterns on the site.

### Personalization score

<Callout icon="📘" theme="info">
  ### Note

  This score only applies if you're using [1:1 Personalization](https://documentation.bloomreach.com/discovery/docs/1-1-personalization).
</Callout>

{user.br} does real-time personalization at a 1:1 level. Each visitor has a unique profile that gets updated in real time based on his/her on-site search, browsing, and purchase behavior. This unique profile is used to compute personalization scores for the retrieved products. For example, if a profile indicates a strong pattern of engaging with men’s products, the men’s products in the retrieved set will receive higher personalization scores and will be ranked higher than women's products.

### Relevance score

The relevance score measures the match of the query to the product. This score is powered by {user.br}'s Semantic Understanding capabilities.

{user.br} computes base relevance using these key factors:

- Extracted product type and attributes from the user's query
- Weighted text match on product fields

For a query such as “red dress”, the {user.br} system understands that the product intent is "dress" with attribute of color "red". All products of type “dress” and attribute "red" will be given a higher relevance score and will be consequently ranked higher than other products that don't match the product type or attribute. The final relevance score will also include some weightage based on the weighted text match on product fields. Surfacing products that exactly match the user intent creates a better purchase experience and also increases conversion rates across your site. 

Here are a few examples that show {user.br}'s Semantic Understanding capabilities:

![](https://files.readme.io/42bfb06-image2017-9-13_21-58-10.png "image2017-9-13_21-58-10.png")

![](https://files.readme.io/b4d5efd-image2017-9-13_21-59-23.png "image2017-9-13_21-59-23.png")

![](https://files.readme.io/1be8de5-image2017-9-13_22-0-51.png "image2017-9-13_22-0-51.png")

For many queries where it is not possible to clearly extract product type, for example “evening wear” or “chromecast”, the weighted text match score is also factored in. When computing the weighted text match, text relevance takes into account many attributes from the product feed and weighs them differently. By default, product title has the highest weight, followed by attributes and category. Description and other searchable fields like keywords carry the lowest weight.

### SKU popularity

{user.br}'s ranking algorithm takes into account user behavior data not just at the product level but also at the SKU level. This is important because, for many apparel products, the popularity of individual SKUs can vary widely. For instance, extreme sizes like XXS and XXL often lag in sales as compared to S, M, and L. Similarly, certain colors might outsell others. When a product's more popular SKUs sell out, that product will start to convert at a lower rate than other similar products where the popular sizes or colors are available. Therefore, when {user.br} detects that the popular SKUs are out of stock for a product, the system automatically lowers the product's overall ranking, which allows other products to move up. 

### Product freshness/recency

Performance ranking signals are based on past user behavior data captured through the {user.br} pixel.  In order to take advantage of more recent user behavior trends, a decay function is applied to the user behavior signals such as views and conversions. This means that conversion for a product that occurred 2 days ago is weighted more heavily than a conversion that occurred 20 days ago. 

This feature means that the engine quickly reacts to changing trends often seen with changing seasons (e.g. fall products converting better than summer), special days (e.g. Mother's Day), special events (e.g. back to school) and new product launches (e.g. launch of a new Chromecast). This results in a better end user experience and higher conversion rate on your site.
