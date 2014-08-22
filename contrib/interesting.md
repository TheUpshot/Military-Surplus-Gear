A File of Interesting Finds People Have Made
=====================================================================
Feel free to contribute but please document your finds reproducibly (line numbers, formulas, SQL statements, etc).

Brevard FL has spent the most at $210,916,922.70, nearly 6 times as much as the second highest spender, Jefferson AL.
```sql
SELECT state, county, SUM(quantity * cost) AS total_cost
  FROM data
 GROUP BY state, county
 ORDER BY total_cost DESC;
```

Arlington VA has $8,047,155.59 in unnamed surplus and there is a total of $28,597,543.91 in unnamed surplus nation wide.
```sql
SELECT state, county, SUM(quantity * cost) AS total_cost
  FROM data
 WHERE item_name IS NULL
 GROUP BY state, county
 ORDER BY total_cost DESC;

SELECT SUM(total_cost) FROM (
    SELECT state, county, SUM(quantity * cost) AS total_cost
      FROM data
     WHERE item_name IS NULL
     GROUP BY state, county
) AS tmp;
```

 year |    total_cost  
----- | ---------------
 2006 |  $34,006,627.64
 2007 |  $16,356,205.62
 2008 |  $51,840,208.53
 2009 |  $80,481,371.64
 2010 |  $99,815,835.16
 2011 | $306,428,186.74
 2012 | $523,555,613.85
 2013 | $531,429,772.96
 2014 | $250,596,770.53

```sql
SELECT EXTRACT(YEAR FROM ship_date) AS year, SUM(quantity * cost) AS total_cost
  FROM data
 GROUP BY year
 ORDER BY year;
```

Although Obama noted during the US presidential debate on October 23rd, 2012 that the military no long longer requires horses and bayonets, the police seem more than happy to pick up those surplus bayonets. The data shows that 12280 bayonets have been purchased.

```sql
SELECT SUM(quantity) FROM data
 WHERE item_name LIKE '%BAYONET%';
```
