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

