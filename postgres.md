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
              ,orderlist.order_dt
    having 300 < sum(fruit.price)
    order by sum(fruit.price)desc;
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

```sql
LEFTは左のテーブルを軸に表示
SELECT *
  FROM person AS p
       LEFT JOIN employee AS e
               ON p.id = e.person_id;
```

```sql
RIGHTは右のテーブルを軸に表示
SELECT *
  FROM person AS p
       RIGHT JOIN employee AS e
               ON p.id = e.person_id;
```

```sql
FULLは全て表示
SELECT *
  FROM person AS p
       FULL JOIN employee AS e
               ON p.id = e.person_id;
```

```sql
INNERは共通するもののみ表示
SELECT *
  FROM person AS p
       INNER JOIN employee AS e
               ON p.id = e.person_id;
```

```sql
crossは２つのテーブルの全ての組み合わせを表示
SELECT *
  FROM person AS p
       CROSS JOIN employee AS e;
```

```sql
employeeに入ってない人を表示する

select *
from person as p
left join employee as e
on p.id=e.person_id
where e.person_id is null;
```

```sql
INを使って一致するものを表示する

select *
from person as p
where id in (select person_id from employee);
 ```

```sql
like:あいまい検索でperson.nameに「ka」を含む人を表示

select *
from person
where person.name like '%ka%';

like 's%'だとsから始まる名前の人を表示
like '%s'だとsで終わる名前の人
```

```sql
exists()で存在するものを表示

select *
from person as p
where exists (select person_id
              from employee
              where person_id=p.id);
```

```sql
distinctで重複を消す

select distinct person.name
      ,fruit.name
      ,fruit.price
from  person
     ,fruit
     ,orderlist
where orderlist.person_id=person.id
 and  orderlist.fruit_id=fruit.id
```

```sql
末尾にoffset(上から何行目以降を表示するか)、
limit(上から最大何行表示するか)をつけて表示する行を指定できる

select person.name
      ,fruit.name
      ,fruit.price
from  person
     ,fruit
     ,orderlist
where orderlist.person_id=person.id
 and  orderlist.fruit_id=fruit.id
group by  person.name
      ,fruit.name
      ,fruit.price
      offset 12  limit 10;
```
