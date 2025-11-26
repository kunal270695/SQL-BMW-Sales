

#1. Explore table

```SQL

Select * from bmw limit 10;

```

| MODEL     | YEAR | REGION        | COLOR  | FUEL_TYPE | TRANSMISSION | ENGINE_SIZE_L | MILEAGE_KM | PRICE_USD | SALES_VOLUME | SALES_CLASSIFICATION |
|-----------|------|---------------|--------|-----------|--------------|----------------|------------|-----------|---------------|-----------------------|
| 5 Series  | 2016 | Asia          | Red    | Petrol    | Manual       | 3.5            | 151748     | 98740     | 8300          | High                 |
| i8        | 2013 | North America | Red    | Hybrid    | Automatic    | 1.6            | 121671     | 79219     | 3428          | Low                  |
| 5 Series  | 2022 | North America | Blue   | Petrol    | Automatic    | 4.5            | 10991      | 113265    | 6994          | Low                  |
| X3        | 2024 | Middle East   | Blue   | Petrol    | Automatic    | 1.7            | 27255      | 60971     | 4047          | Low                  |
| 7 Series  | 2020 | South America | Black  | Diesel    | Manual       | 2.1            | 122131     | 49898     | 3080          | Low                  |
| 5 Series  | 2017 | Middle East   | Silver | Diesel    | Manual       | 1.9            | 171362     | 42926     | 1232          | Low                  |
| i8        | 2022 | Europe        | White  | Diesel    | Manual       | 1.8            | 196741     | 55064     | 7949          | High                 |
| M5        | 2014 | Asia          | Black  | Diesel    | Automatic    | 1.6            | 121156     | 102778    | 632           | Low                  |
| X3        | 2016 | South America | White  | Diesel    | Automatic    | 1.7            | 48073      | 116482    | 8944          | High                 |
| i8        | 2019 | Europe        | White  | Electric  | Manual       | 3.0            | 35700      | 96257     | 4411          | Low                  |
---

**#2. Total records**
``` SQL
Select Count(*) AS total_records from bmw

```

| TOTAL_RECORDS |
|---------------|
| 50000         |
---

**#3. Total Sales**
```SQL

Select SUM(sales_volume) as Total_sales 
from bmw

```

| TOTAL_SALES  |
|--------------|
| 253375734    |
---

**#4. Total revenue**
```SQL
Select SUM(PRICE_USD * SALES_VOLUME) as Total_revenue
from bmw

```

| TOTAL_REVENUE   |
|-----------------|
| 19012242534459  |
---

**#5. Average price**
```SQL
Select AVG(price_usd) as Average_price 
from bmw
```

| AVERAGE_PRICE |
|----------------|
| 75034.600900   |
---

**#6. Sales by year**
```SQL

Select YEAR, SUM(sales_volume) as Total_sales 
from bmw
group by YEAR
Order by YEAR ASC;

```

| YEAR | TOTAL_SALES |
|------|-------------|
| 2010 | 16933445    |
| 2011 | 16758941    |
| 2012 | 16751895    |
| 2013 | 16866733    |
| 2014 | 16958960    |
| 2015 | 17010207    |
| 2016 | 16957550    |
| 2017 | 16620811    |
| 2018 | 16412273    |
| 2019 | 17191956    |
| 2020 | 16310843    |
| 2021 | 16884666    |
| 2022 | 17920946    |
| 2023 | 16268654    |
| 2024 | 17527854    |
---

**#7. Sales by model**
```SQL

Select b.model, SUM(b.SALES_VOLUME) as Total_sales
from bmw as b
GROUP by b.MODEL
Order by Total_sales DESC;

```

| MODEL     | TOTAL_SALES |
|-----------|-------------|
| 7 Series  | 23786466    |
| i8        | 23423891    |
| X1        | 23406060    |
| 3 Series  | 23281303    |
| i3        | 23133849    |
| 5 Series  | 23097519    |
| M5        | 22779688    |
| X3        | 22745529    |
| X5        | 22709749    |
| X6        | 22661986    |
| M3        | 22349694    |
---

**#8. Hybrid car percent**
```SQL

Select 100.00 * SUM(Case when fuel_type in ('Electric', 'Hybrid') Then sales_volume Else 0 END) / 
    SUM(sales_volume) as Hybrid_electric_percent
from bmw;
```

| HYBRID_ELECTRIC_PERCENT |
|--------------------------|
| 50.395419                |
---

**#9. Sales by region**
```SQL

Select Region, Sum(sales_volume) Total_sales
from bmw
group by REGION
order by region DESC;

```

| REGION        | TOTAL_SALES |
|---------------|-------------|
| South America | 41,551,818  |
| North America | 42,402,629  |
| Middle East   | 42,326,620  |
| Europe        | 42,555,138  |
| Asia          | 42,974,277  |
| Africa        | 41,565,252  |
---

**#10. Model by top sales**

``` SQL
Select b.model, SUM(b.SALES_VOLUME) as Total_sales
from bmw as b
GROUP by b.MODEL
Order by Total_sales DESC
Limit 1;

```

| MODEL    | TOTAL_SALES |
|----------|-------------|
| 7 Series | 23,786,466  |
---

**11. Revenue by region**

``` SQL
Select Region, SUM(price_USD * sales_volume) as Total_revenue, SUM(sales_volume) as Total_sales
from bmw
group by REGION
Order by Total_revenue;
```

| REGION        | TOTAL_REVENUE     | TOTAL_SALES |
|---------------|-------------------|-------------|
| Africa        | 3,108,999,419,352 | 41,565,252  |
| South America | 3,113,805,414,620 | 41,551,818  |
| Middle East   | 3,167,783,530,851 | 42,326,620  |
| North America | 3,182,938,635,076 | 42,402,629  |
| Europe        | 3,188,079,573,212 | 42,555,138  |
| Asia          | 3,250,635,961,348 | 42,974,277  |
---

**12. Average engine size**

```SQL

Select ROUND(AVG(ENgine_Size_L), 1) as Average_engine_size
from bmw
```

| AVERAGE_ENGINE_SIZE |
|---------------------|
| 3.2                 |
---

**13. Sales by Average engine size**

```SQL
Select SUM(sales_volume) as Total_sales, AVG(ENgine_Size_L)
from bmw
Group by region
order by Total_sales DESC;
```

| TOTAL_SALES | AVG_ENGINE_SIZE_L |
|-------------|-------------------|
| 42,974,277  | 3.2315709          |
| 42,555,138  | 3.2381929          |
| 42,402,629  | 3.2497660          |
| 42,326,620  | 3.2561567          |
| 41,565,252  | 3.2581243          |
| 41,551,818  | 3.2495819          |
---


**14. Top 10 models by revenue**

```SQL
Select Model, SUM(Price_USD * sales_volume) as Total_revenue
from bmw 
Group by MODEL
Order by Total_revenue DESC;
```

| MODEL     | TOTAL_REVENUE     |
|-----------|-------------------|
| 7 Series  | 1,790,070,249,282 |
| 3 Series  | 1,768,534,028,214 |
| i8        | 1,764,743,448,529 |
| X1        | 1,752,985,285,361 |
| 5 Series  | 1,735,712,423,092 |
| i3        | 1,724,197,530,210 |
| X5        | 1,708,653,383,772 |
| X3        | 1,707,951,188,482 |
| M5        | 1,698,467,355,916 |
| X6        | 1,693,423,254,979 |
| M3        | 1,667,504,386,622 |
---


**15.  Top 10 models by revenue and sales in Asia**


```SQL
Select Model, SUM(Price_USD * sales_volume) as Total_revenue, SUM(SALES_VOLUME) as Total_sales
from bmw 
where REGION = 'Asia'
Group by MODEL
Order by Total_revenue DESC;
```

| MODEL     | TOTAL_REVENUE     | TOTAL_SALES |
|-----------|-------------------|-------------|
| X1        | 310,980,489,459   | 4,192,289   |
| 7 Series  | 304,097,565,188   | 4,004,066   |
| M3        | 304,012,053,648   | 3,935,579   |
| 3 Series  | 302,685,161,456   | 3,962,239   |
| i8        | 301,658,766,540   | 3,975,942   |
| M5        | 294,331,241,200   | 3,928,390   |
| X3        | 292,717,213,333   | 3,796,115   |
| 5 Series  | 291,989,135,417   | 3,935,629   |
| X6        | 284,615,674,622   | 3,756,074   |
| i3        | 283,878,059,602   | 3,739,218   |
| X5        | 279,670,600,883   | 3,748,736   |
---


**16. Top 10 models by revenue and sales in Europe**
```SQL
Select Model, SUM(Price_USD * sales_volume) as Total_revenue, SUM(SALES_VOLUME) as Total_sales
from bmw 
where REGION = 'Europe'
Group by MODEL
Order by Total_revenue DESC;
```

| MODEL     | TOTAL_REVENUE     | TOTAL_SALES |
|-----------|-------------------|-------------|
| i8        | 322,248,193,289   | 4,202,401   |
| 3 Series  | 304,196,796,025   | 3,959,930   |
| i3        | 294,806,039,279   | 3,954,257   |
| M5        | 294,088,330,593   | 4,002,667   |
| 5 Series  | 291,699,397,601   | 3,855,515   |
| 7 Series  | 289,881,216,749   | 3,914,409   |
| X5        | 283,787,379,840   | 3,688,138   |
| X1        | 283,759,876,726   | 3,850,033   |
| X6        | 279,585,786,666   | 3,772,519   |
| X3        | 275,829,016,944   | 3,705,572   |
| M3        | 268,197,539,500   | 3,649,697   |
---


**17. Sales by fuel type**

```SQL
Select Fuel_type, SUM(Price_USD * sales_volume) as Total_revenue, SUM(SALES_VOLUME)
from bmw
group by FUEL_TYPE
Order by Total_revenue
```

| FUEL_TYPE | TOTAL_REVENUE     | TOTAL_SALES  |
|-----------|-------------------|--------------|
| Diesel    | 4,684,699,087,721 | 62,361,818   |
| Electric  | 4,750,735,161,530 | 63,157,665   |
| Petrol    | 4,756,136,615,908 | 63,324,154   |
| Hybrid    | 4,820,671,669,300 | 64,532,097   |
---


**18. Highest price car** 

```SQL
Select Model, price_usd as Price, Region
from bmw
Order by price_usd DESC
limit 5;
```

| MODEL     | PRICE   | REGION       |
|-----------|---------|--------------|
| i8        | 119,998 | Middle East  |
| X6        | 119,997 | Asia         |
| i8        | 119,997 | Africa       |
| X1        | 119,996 | Africa       |
| 3 Series  | 119,994 | Middle East  |
---


**19. Lowest price car**
```SQL
Select Model, Price_usd as Price, Region
from bmw
Order by price_usd ASC
Limit 5;
```

| MODEL | PRICE | REGION |
| --- | --- | --- |
| i8 | 30000 | Asia |
| X5 | 30001 | Asia |
| 5 Series | 30002 | Africa |
| M5 | 30005 | Asia |
| 3 Series | 30008 | Middle East |
---


**20. Average price of models in last 5 years**

```SQL
Select Year, Model, AVG(Price_usd) as Average_price
from bmw
where year between 2019 and 2024
Group by Year, MODEL
Order by Year ASC;
```

| YEAR | MODEL | AVERAGE_PRICE |
| --- | --- | --- |
| 2019 | X5 | 74103.030675 |
| 2019 | X3 | 74817.667763 |
| 2019 | X1 | 74955.076696 |
| 2019 | X6 | 73474.299094 |
| 2019 | i3 | 75496.466667 |
| 2019 | M3 | 74763.985663 |
| 2019 | 5 Series | 74325.133333 |
| 2019 | 3 Series | 76310.783505 |
| 2019 | 7 Series | 77551.142857 |
| 2019 | i8 | 75952.479310 |
| 2019 | M5 | 75824.695238 |
| 2020 | i8 | 75819.689895 |
| 2020 | i3 | 74706.666667 |
| 2020 | X1 | 73369.131410 |
| 2020 | 5 Series | 76141.335505 |
| 2020 | 7 Series | 73016.311475 |
| 2020 | M3 | 76541.420690 |
| 2020 | X6 | 73780.176678 |
| 2020 | 3 Series | 77888.274576 |
| 2020 | X3 | 75590.033088 |
| 2020 | X5 | 72784.247350 |
| 2020 | M5 | 76053.438356 |
| 2021 | X1 | 77652.370629 |
| 2021 | M3 | 75954.802632 |
| 2021 | M5 | 74543.304615 |
| 2021 | X6 | 74755.412903 |
| 2021 | i3 | 74687.108434 |
| 2021 | X5 | 76211.174377 |
| 2021 | 3 Series | 75743.006192 |
| 2021 | i8 | 74907.394558 |
| 2021 | X3 | 75945.557047 |
| 2021 | 7 Series | 74132.083333 |
| 2021 | 5 Series | 75243.993220 |
| 2022 | 3 Series | 74994.996815 |
| 2022 | 7 Series | 74480.639394 |
| 2022 | X3 | 74167.547692 |
| 2022 | i3 | 74975.359736 |
| 2022 | M3 | 74534.213376 |
| 2022 | 5 Series | 75215.752475 |
| 2022 | i8 | 73369.700000 |
| 2022 | X1 | 75867.663462 |
| 2022 | X5 | 73899.469388 |
| 2022 | X6 | 76172.614679 |
| 2022 | M5 | 77184.670034 |
| 2023 | M5 | 73330.069686 |
| 2023 | X3 | 72929.650519 |
| 2023 | X1 | 76227.155477 |
| 2023 | i8 | 76119.940789 |
| 2023 | 5 Series | 76061.195205 |
| 2023 | i3 | 74171.352113 |
| 2023 | 7 Series | 76240.239482 |
| 2023 | M3 | 77326.045752 |
| 2023 | 3 Series | 76426.518395 |
| 2023 | X5 | 74275.562963 |
| 2023 | X6 | 73695.564189 |
| 2024 | 3 Series | 76603.288591 |
| 2024 | X5 | 73870.366548 |
| 2024 | 5 Series | 75527.853659 |
| 2024 | 7 Series | 75333.679878 |
| 2024 | M3 | 72894.577206 |
| 2024 | i8 | 76449.084416 |
| 2024 | i3 | 73823.232416 |
| 2024 | M5 | 72393.318612 |
| 2024 | X1 | 75472.973333 |
| 2024 | X6 | 76078.495652 |
| 2024 | X3 | 76452.529412 |
---

**21. Top 5 most expensive models**

```SQL
Select Model, MAX(price_usd) as Price
from bmw
Group by Model
Order by Price DESC
Limit 5;
```

| MODEL | PRICE |
| --- | --- |
| i8 | 119998 |
| X6 | 119997 |
| X1 | 119996 |
| 3 Series | 119994 |
| 5 Series | 119988 |
---


**22. Sales trend by year**

```SQL
Select Year, SUM(Sales_volume) as Total_sales
from bmw
group by year
Order by year ASC;
```

| YEAR | TOTAL_SALES |
| --- | --- |
| 2010 | 16933445 |
| 2011 | 16758941 |
| 2012 | 16751895 |
| 2013 | 16866733 |
| 2014 | 16958960 |
| 2015 | 17010207 |
| 2016 | 16957550 |
| 2017 | 16620811 |
| 2018 | 16412273 |
| 2019 | 17191956 |
| 2020 | 16310843 |
| 2021 | 16884666 |
| 2022 | 17920946 |
| 2023 | 16268654 |
| 2024 | 17527854 |
---

**23. revenue by region **

```SQL
Select Region, SUM(price_usd * Sales_volume) as Total_revenue
from bmw
Group by region
Order by Total_revenue DESC;
```

| REGION | TOTAL_REVENUE |
| --- | --- |
| Asia | 3250635961348 |
| Europe | 3188079573212 |
| North America | 3182938635076 |
| Middle East | 3167783530851 |
| South America | 3113805414620 |
| Africa | 3108999419352 |
---

**24. Price difference between fuel types **
```SQL
Select MAX(Price_usd) - MIN(Price_usd) as Price_difference
from bmw 
where fuel_type in ('Electric', 'Petrol')
```

| PRICE_DIFFERENCE |
| --- |
| 89998 |
---

**25. Best selling model per year **

```SQL

Select year, model, Total_sales
from (
    Select
        year,
        model,
        SUM(Sales_Volume) AS Total_sales,
        RANK() OVER (PARTITION BY year ORDER BY SUM(Sales_Volume) DESC) AS rnk
    from bmw
    group by YEAR, model
) t
where rnk = 1
ORDER BY Year;
```

| YEAR | MODEL | TOTAL_SALES |
| --- | --- | --- |
| 2010 | 3 Series | 1647769 |
| 2011 | X1 | 1694495 |
| 2012 | i3 | 1752148 |
| 2013 | X1 | 1730904 |
| 2014 | 3 Series | 1682545 |
| 2015 | 7 Series | 1683339 |
| 2016 | 3 Series | 1712098 |
| 2017 | 7 Series | 1763339 |
| 2018 | i8 | 1623682 |
| 2019 | X1 | 1681721 |
| 2020 | X1 | 1618766 |
| 2021 | M5 | 1689063 |
| 2022 | X5 | 1796846 |
| 2023 | 7 Series | 1583848 |
| 2024 | X6 | 1836396 |
---

**26. Engine size vs Average price**

```SQL
Select Engine_size_l as Engine_size, Round(AVG(Price_usd),2) as Average_price, Round(AVG(sales_volume),0) as Avg_sales
from bmw
group by Engine_size
Order by Engine_size ASC;
```

| ENGINE_SIZE | AVERAGE_PRICE | AVG_SALES |
| --- | --- | --- |
| 1.5 | 74680.55 | 5051 |
| 1.6 | 74801.10 | 5084 |
| 1.7 | 75102.73 | 5019 |
| 1.8 | 74099.34 | 5054 |
| 1.9 | 75174.27 | 5212 |
| 2.0 | 74812.07 | 5104 |
| 2.1 | 76116.76 | 5045 |
| 2.2 | 74631.16 | 4996 |
| 2.3 | 74028.73 | 5034 |
| 2.4 | 75293.58 | 5114 |
| 2.5 | 75667.32 | 5088 |
| 2.6 | 75416.54 | 5050 |
| 2.7 | 74527.37 | 5158 |
| 2.8 | 75336.09 | 5029 |
| 2.9 | 74621.15 | 5028 |
| 3.0 | 75102.96 | 5154 |
| 3.1 | 74072.15 | 5053 |
| 3.2 | 75227.32 | 5256 |
| 3.3 | 75277.59 | 4932 |
| 3.4 | 75800.00 | 5227 |
| 3.5 | 75323.00 | 5027 |
| 3.6 | 76263.54 | 4951 |
| 3.7 | 74767.88 | 5126 |
| 3.8 | 75356.58 | 5012 |
| 3.9 | 75923.88 | 5070 |
| 4.0 | 74391.45 | 4928 |
| 4.1 | 75313.01 | 4999 |
| 4.2 | 76170.33 | 5097 |
| 4.3 | 74455.97 | 5168 |
| 4.4 | 75710.49 | 5032 |
| 4.5 | 73109.52 | 5191 |
| 4.6 | 75176.16 | 4924 |
| 4.7 | 75613.46 | 5154 |
| 4.8 | 74313.78 | 4988 |
| 4.9 | 75260.39 | 4991 |
| 5.0 | 73261.76 | 5040 |
---
