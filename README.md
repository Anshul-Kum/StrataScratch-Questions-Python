# StrataScratch-Questions-Python

### [Amazon | Easy | Products with No Sales](https://platform.stratascratch.com/coding/2109-products-with-no-sales?code_type=2)

Write a query to get a list of products that have not had any sales. Output the ID and market name of these products.

```python
# Import your libraries
import pandas as pd

# Start writing code
fct_customer_sales.head()
dim_product.head()
res = fct_customer_sales.merge(dim_product, on = 'prod_sku_id',how = 'right')
res[res['order_value'].isna()][['prod_sku_id', 'market_name']]
```
### [Apple | Easy | Find the date with the highest opening stock price](https://platform.stratascratch.com/coding/9613-find-the-date-with-the-highest-opening-stock-price?code_type=2)

Find the date when Apple's opening stock price reached its maximum.

```python
# Import your libraries
import pandas as pd

# Start writing code
aapl_historical_stock_price.head()
aapl_historical_stock_price['date'] = aapl_historical_stock_price['date'].apply(lambda x: x.strftime('%Y-%m-%d'))
aapl_historical_stock_price[aapl_historical_stock_price['open'] == aapl_historical_stock_price['open'].max()][['date', 'open']]
```
### [Amazon | Medium | The Most Expensive Products Per Category](https://platform.stratascratch.com/coding/9607-the-most-expensive-products-per-category?code_type=2)

Find the most expensive products on Amazon for each product category. Output category, product name and the price (as a number).

```python
# Import your libraries
import pandas as pd

# Start writing code
innerwear_amazon_com.head()
innerwear_amazon_com['price'] = innerwear_amazon_com['price'].replace(
    '[\$,]', '', regex=True).astype(float)
innerwear_amazon_com.loc[innerwear_amazon_com.groupby(['product_category'])['price'].idxmax(), ['product_category', 'product_name', 'price']]
```
### [Wine Magazine | Medium | Macedonian Vintages](https://platform.stratascratch.com/coding/10039-macedonian-vintages?code_type=2)

Find the vintage years of all wines from the country of Macedonia. The year can be found in the 'title' column. Output the wine (i.e., the 'title') along with the year. The year should be a numeric or int data type.

```python
# Import your libraries
import pandas as pd
import re
# Start writing code
winemag_p2.head()
def year(string):
    yr = re.search(r'\d{4}', string)
    if yr != None:
        return yr.group()
    else:
        return 0

winemag_p2['year'] = winemag_p2['title'].apply(year)
winemag_p2['year'] = winemag_p2['year'].astype('int')
winemag_p2[['title', 'year']]
```

### [City of San Francisco | Medium | Find all businesses whose lowest and highest inspection scores are different](https://platform.stratascratch.com/coding/9731-find-all-businesses-whose-lowest-and-highest-inspection-scores-are-different?code_type=2)

Find all businesses whose lowest and highest inspection scores are different.
Output the corresponding business name and the lowest and highest scores of each business. HINT: you can assume there are no different businesses that share the same business name
Order the result based on the business name in ascending order.

```python
# Import your libraries
import pandas as pd

# Start writing code
sf_restaurant_health_violations.head()
diff = sf_restaurant_health_violations.groupby('business_name')['inspection_score'].agg(min_score = 'min', max_score = 'max').reset_index()
res = diff[diff['min_score'] != diff['max_score']]
res = res.dropna()
res = res.sort_values('business_name')
res
```
