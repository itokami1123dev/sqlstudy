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
