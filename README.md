## Лобанчиков Леонид Дмитриевич
### Ссылка на весь код(создание таблиц) - https://sqlize.online/sql/mysql80/0ecd8a4b241ea99b1afd04955b198f42/

### Решение задач подробно
***

## 4.
  Сформируйте отчет, который содержит все счета, относящиеся к продуктам <br>типа ДЕПОЗИТ, принадлежащих клиентам, у которых нет открытых продуктов типа КРЕДИТ.<br>
  
<br>select * from (
<br>&nbsp;	select * from accounts
<br>&nbsp;&nbsp;&nbsp;		where (product_ref = 1 or product_ref = 2) AND close_date is null
<br>&nbsp;&nbsp;&nbsp;		Order by client_ref, product_ref) as acc
<br>&nbsp;	group by acc.client_ref
<br>&nbsp;	having acc.product_ref != 1;
##### Решение: <br> Подзапросом я получаю всех клиентов, у кого есть открытые депозиты и открытые кредиты.<br> Группирую. Группировка оставляет у клиента одну запись<br> Если у клиента не было кредитов, у него останется 2(Депозит) в product_ref.

## 5.
Сформируйте выборку, который содержит средние движения по счетам в рамках одного произвольного дня, в разрезе типа продукта.
<br>
<br>select accounts.id, accounts.name, accounts.acc_num,records.dt, records.sum, records.acc_ref, records.oper_date, accounts.product_ref
<br>&nbsp;&nbsp;		from accounts INNER JOIN records on records.acc_ref = accounts.id
<br>&nbsp;&nbsp;	where oper_date = '2015-10-01' and product_ref = 1;
