postgres練習
------------

```sql
select fruit.name
from fruit;
```

```sql
select *
from person
    ,fruit
    ,orderlist
    where orderlist.person_id=person.id
    and  orderlist.fruit_id=fruit.id;
```

```sql
select fruit.name
      ,person.name
 from fruit
     ,person
     ,orderlist
where orderlist.person_id=person.id
and  orderlist.fruit_id=fruit.id
and=person.id=5
```

```sql
select person.name
      ,fruit.name
      ,SUM(fruit.price)
      ,count(*)
 from fruit
     ,person
     ,orderlist
where orderlist.person_id=person.id
and  orderlist.fruit_id=fruit.id
and person.id=5
GROUP BY person.name,fruit.name
```

```sql
select person.name
      ,fruit.name
      ,SUM(fruit.price)
      ,count(*)
from  fruit
     ,person
     ,orderlist
where orderlist.person_id=person.id
and  orderlist.fruit_id=fruit.id
and person.id=3
GROUP BY person.name,fruit.name
```
```sql
select *
 from(select fruit.name as fruit_name
        ,sum(fruit.price)
        ,person.name
      from fruit
        ,person
        ,orderlist
      where orderlist.person_id=person.id
            and  orderlist.fruit_id=fruit.id
            and person.id=5
     GROUP BY fruit.name
              ,person.name
     )AS tbl1
LEFT JOIN (
            select fruit.name as fruit_name
              ,sum(fruit.price)
              ,person.name
            from fruit
              ,person
              ,orderlist
            where orderlist.person_id=person.id
                  and orderlist.fruit_id=fruit.id
                  and person.id=3
            GROUP BY fruit.name
              ,person.name
          )AS tbl2
ON tbl1.fruit_name=tbl2.fruit_name;
```

```sql
alter table orderlist add order_dt date;
```

```sql
select tax_str_dt
       ,tax_end_dt
       ,tax_rate
from tax
where tax_str_dt <= '2014-04-01'
and   tax_end_dt >= '2014-04-01'
```

```sql
select *
from tax
where '2014-04-01' between tax_str_dt and tax_end_dt;
```

```sql
select order_dt
,tax_rate
from tax
,orderlist
where orderlist.order_dt between tax.tax_str_dt and tax_end_dt
;
```

```sql
select fruit.name
       ,fruit.price
       ,tax.tax_rate
       ,round(fruit.price * tax.tax_rate/100)
       +fruit.price
 from fruit
         ,tax
where '2015-03-25' between tax. tax_str_dt and tax_end_dt;
```

```sql
select person.name
        ,fruit.name as fruit_name
        ,sum(fruit.price)
        ,tax.tax_rate
        ,round(fruit.price * tax.tax_rate/100)
        +fruit.price
        ,orderlist.order_dt
      from fruit
        ,person
        ,orderlist
        ,tax
      where orderlist.person_id=person.id
            and  orderlist.fruit_id=fruit.id
            and person.id=5
            and orderlist.order_dt between tax. tax_str_dt and tax_end_dt
     GROUP BY fruit.name
              ,person.name
              ,fruit.price
              ,tax.tax_rate
              ,orderlist.order_dt;
```

```sql
select person.name
      ,sum(fruit.price)
      ,min(fruit.price)
      ,max(fruit.price)
      ,round(avg(fruit.price))
from person
    ,fruit
    ,orderlist
where orderlist.person_id=person.id
 and orderlist.fruit_id=fruit.id
group by person.name;
```

