## Лобанчиков Леонид Дмитриевич
### База данных - МySQL 8.0
<br>create table tarifs(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	NAME VARCHAR(100),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	COST DECIMAL(10.2)
<br>	);
<br>create table clients(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	NAME VARCHAR(1000),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	PLACE_OF_BIRTH VARCHAR(1000),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	DATE_OF_BIRTH date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ADDRESS VARCHAR(1000),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	PASSPORT VARCHAR(1000)
<br>	);
<br>create table productype(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	NAME VARCHAR(100),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	BEGIN_DATE date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	END_DATE date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	TARIF_REF int(10),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	FOREIGN KEY (TARIF_REF) REFERENCES tarifs(ID)
<br>	);
<br>CREATE table products(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	PRODUCT_TYPE_ID int(10),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	foreign key (PRODUCT_TYPE_ID)  REFERENCES productype(ID),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	name VARCHAR(100),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	CLIENT_REF int(10),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	foreign key (CLIENT_REF) REFERENCES clients(ID),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	OPEN_DATE date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	CLOSE_DATE date
<br>);
<br>
<br>CREATE table accounts(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	NAME VARCHAR(100),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	SALDO decimal(10,2),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	CLIENT_REF int(10),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	foreign key (CLIENT_REF) REFERENCES clients(ID),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	OPEN_DATE date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	CLOSE_DATE date,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	PRODUCT_REF int(100),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	foreign key (PRODUCT_REF) REFERENCES  products(PRODUCT_TYPE_ID),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ACC_NUM VARCHAR(25) 
<br>	);
<br>CREATE table records(
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ID int(10) primary key,
<br>&nbsp;&nbsp;&nbsp;&nbsp;	DT int(1),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	SUM DECIMAL(10,2),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	ACC_REF int(20),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	foreign key (ACC_REF) REFERENCES accounts(ID),
<br>&nbsp;&nbsp;&nbsp;&nbsp;	OPER_DATE date
<br>);
<br>insert into tarifs values (1,'Тариф за выдачу кредита', 10);
<br>insert into tarifs values (2,'Тариф за открытие счета', 10);
<br>insert into tarifs values (3,'Тариф за обслуживание карты', 10);
<br>  
<br>insert into clients values (1, 'Сидоров Иван Петрович', 'Россия, Московская облать, г. Пушкин', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать,г. Пушкин, ул. Грибоедова, д. 5', '2222 555555, выдан ОВД г. Пушкин, 10.01.2015');
<br>insert into clients values (2, 'Иванов Петр Сидорович', 'Россия, Московская облать, г. Клин', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать,г. Клин, ул. Мясникова, д. 3', '4444 666666, выдан ОВД г. Клин, 10.01.2015');
<br>insert into clients values (3, 'Агат Сиодр Иванович', 'Россия, Московская облать, г. ВВВ', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать, г.Балашиха, ул. Пушкина, д. 7', '4444 662326, выдан ОВД г. Клин, 10.01.2015');
<br>
<br>insert into productype values (1, 'КРЕДИТ', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 1);
<br>insert into productype values (2,  'ДЕПОЗИТ', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 2);
<br>insert into productype values (3,  'КАРТА', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 3);
<br>
<br>insert into products values (1, 1, 'Кредитный договор с Сидоровым И.П.', 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'), null);
<br>insert into products values (2, 2, 'Депозитный договор с Ивановым П.С.', 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null);
<br>insert into products values (3, 3, 'Карточный договор с Петровым С.И.', 3, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null);
<br>insert into products values (5, 1, 'Кредитный договор с Петровым С.И.', 3, STR_TO_DATE('01.08.2022','%d.%m.%Y'), STR_TO_DATE('05.09.2022','%d.%m.%Y'));
<br>insert into products values (4, 1, 'Кредитный договор с Сидоровым И.П.', 1, STR_TO_DATE('05.09.2022','%d.%m.%Y'), null);
<br>
<br>insert into accounts values (1, 'Кредитный счет для Сидоровым И.П.', -1000, 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'), null, 1, '45502810401020000022');
<br>insert into accounts values (2, 'Депозитный счет для Ивановым П.С.', 44000, 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null, 2, '42301810400000000001');
<br>insert into accounts values (3, 'Карточный счет для Петровым С.И.', 125000, 3, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null, 3, '40817810700000000001');
<br>insert into accounts values (4, 'Кредитный счет для Ивановым П.С.', -3000, 2, STR_TO_DATE('02.08.2017','%d.%m.%Y'), null, 1, '42301810400000000023');
<br>insert into accounts values (5, 'Депозитный счет для Петровым С.И.', 4000, 3, STR_TO_DATE('02.08.2017','%d.%m.%Y'), null, 2, '40817810700000000024');
<br>insert into records values (1, 1, 5000, 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'));
<br>insert into records values (2, 0, 1000, 1, STR_TO_DATE('01.07.2015','%d.%m.%Y'));
<br>insert into records values (3, 0, 2000, 1, STR_TO_DATE('01.08.2015','%d.%m.%Y'));
<br>insert into records values (4, 0, 3000, 1, STR_TO_DATE('01.09.2015','%d.%m.%Y'));
<br>insert into records values (5, 1, 5000, 1, STR_TO_DATE('01.10.2015','%d.%m.%Y'));
<br>
<br>insert into records values (6, 0, 3000, 1, STR_TO_DATE('01.10.2015','%d.%m.%Y'));
<br>
<br>insert into records values (7, 0, 10000, 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'));
<br>insert into records values (8, 1, 1000, 2, STR_TO_DATE('05.08.2017','%d.%m.%Y'));
<br>insert into records values (9, 1, 2000, 2, STR_TO_DATE('21.09.2017','%d.%m.%Y'));
<br>
<br>insert into records values (10, 1, 5000, 2, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>insert into records values (12, 0, 120000, 3, STR_TO_DATE('08.09.2017','%d.%m.%Y'));
<br>insert into records values (13, 1, 1000, 3, STR_TO_DATE('05.10.2017','%d.%m.%Y'));
<br>insert into records values (11, 0, 6000, 2, STR_TO_DATE('26.11.2017','%d.%m.%Y'));
<br>insert into records values (14, 1, 2000, 3, STR_TO_DATE('21.10.2017','%d.%m.%Y'));
<br>insert into records values (15, 1, 5000, 3, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>insert into records values (16, 0, 3000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
<br>insert into records values (17, 1, 3000, 3, STR_TO_DATE('24.08.2022','%d.%m.%Y'));
<br>insert into records values (18, 1, 5000, 4, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>insert into records values (19, 0, 5000, 5, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>insert into records values (20, 0, 2000, 4, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>insert into records values (21, 1, 1000, 5, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
<br>
<br>insert into records values (22, 0, 11000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
<br>insert into records values (23, 0, 12000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
<br>insert into records values (24, 0, 13000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
<br>insert into records values (25, 0, 4000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
<br>insert into records values (26, 0, 5000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
<br>insert into records values (27, 0, 3000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
<br>insert into records values (28, 0, 1000, 3, STR_TO_DATE('1.09.2022','%d.%m.%Y'));
<br>
<br>
## 4.
  Сформируйте отчет, который содержит все счета, относящиеся к продуктам <br>типа ДЕПОЗИТ, принадлежащих клиентам, у которых нет открытых продуктов типа КРЕДИТ.<br>
  
<br>select * from (
<br>&nbsp;	***select * from accounts
<br>&nbsp;&nbsp;&nbsp;		where (product_ref = 1 or product_ref = 2) AND close_date is null
<br>&nbsp;&nbsp;&nbsp;		Order by client_ref, product_ref***) as acc
<br>&nbsp;	group by acc.client_ref
<br>&nbsp;	having acc.product_ref != 1;
##### Решение: <br> Подзапросом я получаю всех клиентов, у кого есть открытые депозиты и открытые кредиты.<br> Группирую. Группировка оставляет у клиента одну запись<br> Если у клиента не было кредитов, у него останется 2(Депозит) в product_ref.
<br>Что отдает подзапрос
![Screenshot_5](https://user-images.githubusercontent.com/113181404/189364761-6b48e952-d97b-4451-b52c-e60d96eb0040.png)
<br>Результат
![Screenshot_3](https://user-images.githubusercontent.com/113181404/189364460-59fa03ff-6f25-4603-9769-b2d39191686d.png)

## 5.
Сформируйте выборку, которая содержит средние движения по счетам в рамках одного произвольного дня, в разрезе типа продукта.
<br>
<br>select accounts.id, accounts.name, accounts.acc_num, records.acc_ref, records.oper_date, accounts.product_ref
<br>&nbsp;&nbsp;&nbsp;		from accounts INNER JOIN records on records.acc_ref = accounts.id
<br>&nbsp;&nbsp;&nbsp;	where oper_date = '2015-10-01' and product_ref = 1;
<br>
##### Решение: <br> Cклеил две таблицы inner join и отсортировал их по дате и типу продукта.
Результат<br>
![Screenshot_3](https://user-images.githubusercontent.com/113181404/189371394-755477d7-864a-44fd-b16a-4769f5f63fb5.png)

## 6.
Сформируйте выборку, в который попадут клиенты, у которых были операции по счетам <br>за прошедший месяц от текущей даты. Выведите клиента и сумму операций за день в разрезе даты.
<br>
<br>select accounts.id, accounts.name, records.oper_date, count(1) as Количество операций
<br>&nbsp;&nbsp;	from accounts
<br>&nbsp;&nbsp;	INNER JOIN records on records.acc_ref = accounts.id
<br>&nbsp;&nbsp;	where to_days(now()) - to_days(oper_date) <= 30
<br>&nbsp;&nbsp;	group by accounts.name, records.oper_date
##### Решение: соединяю две таблицы. Каждую дату вычитаю из сегодняшней, получаю число. Добавляю count(1) и группирую
<br>Результат<br>
![Screenshot_3](https://user-images.githubusercontent.com/113181404/189374042-777379f0-3782-4841-bd9f-09461f573cb3.png)
## 7.
В результате сбоя в базе данных разъехалась информация между остатками и операциями <br>по счетам. Напишите нормализацию (процедуру выравнивающую данные), которая найдет такие <br>счета и восстановит остатки по счету.
<br>
<br>select * from accounts;
<br>UPDATE accounts as a1, records as a2
<br>SET a1.saldo = (select a3.sam 
<br>&nbsp;&nbsp;                        from (select sum(sum) as sam, dt, acc_ref 
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                              from records 
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                             group by acc_ref, dt) as a3
<br>&nbsp;&nbsp;                       where a3.dt = 0 AND a1.id = a3.acc_ref) 
<br>&nbsp;&nbsp;                        - 
<br>&nbsp;&nbsp;                        (select a4.sumi 
<br>&nbsp;&nbsp;                         from (select sum(sum) as sumi, dt, acc_ref 
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                               from records 
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                               group by acc_ref, dt) as a4
<br>&nbsp;&nbsp;                         where a4.dt = 1 AND a1.id = a4.acc_ref)
<br>where a1.id = a2.acc_ref; <br><br>
***Решение: в таблице records, в столбике dt указаны значения операций. 0 - пополнение. 1 - снятие. Я сгруппировал все пополнения и снятия, а потом вычел второе из первого. У меня получились корректные данные на основе истории транзакций***<br>
<br>Добавил всем по 10000 
![Screenshot_2](https://user-images.githubusercontent.com/113181404/189375913-8b80df72-2ca5-4e5d-84a5-9938f0d7676b.png)
<br>Результат
![Screenshot_5](https://user-images.githubusercontent.com/113181404/189376034-22b9ac7a-9755-4b44-872a-6c98ec0ecbcb.png)
## 8.
Сформируйте выборку, который содержит информацию о клиентах, которые полностью погасили кредит, но при этом не закрыли продукт и пользуются им дальше (по продукту есть операция новой выдачи кредита).
<br>
<br>select *
<br>&nbsp;&nbsp;from (select * from (select client_ref, name  from products where product_type_id = 1 AND close_date is not null group by client_ref, <br>&nbsp;&nbsp;name) as a1
<br>&nbsp;&nbsp;&nbsp;&nbsp;        union all
<br>&nbsp;&nbsp;        select * from (select client_ref, name  from products where product_type_id = 1 AND close_date is null group by client_ref, name) <br>&nbsp;&nbsp;as a2) as a3
<br>group by a3.client_ref, a3.name
<br>having count(1) > 1
##### Решение:<br> В первом подзапросе клиенты с закрытым кредитом. Во втором - с открытым кредитом. Кто попадает в обе группы - результат
<br>Объединенная таблица union all<br>
![Screenshot_2](https://user-images.githubusercontent.com/113181404/189382534-8f98e997-4f70-4629-ab9e-66685f39bd81.png)
<br>Результат<br>
![Screenshot_3](https://user-images.githubusercontent.com/113181404/189382540-13adfaeb-ee0e-4cf6-9c72-6b069e3557a0.png)
## 9.
## 10.
Закройте возможность открытия (установите дату окончания действия) для типов продуктов, по счетам продуктов которых, не было движений более одного месяца.<br>
<br>update accounts as a1
<br>set a1.close_date = CURRENT_DATE(); 
<br>where to_days(NOW()) - TO_DAYS(
<br>&nbsp;&nbsp;&nbsp;&nbsp;            (select a2.oper
<br>&nbsp;&nbsp;&nbsp;&nbsp;            from (select max(oper_date) as oper,acc_ref from records group by acc_ref) as a2
<br>&nbsp;&nbsp;&nbsp;&nbsp;            where  a1.id = a2.acc_ref)) >= 30;
<br>
##### Решение:<br> Из таблицы с последней датой достаем дату по каждому счету. Вычитаем её из сегодняшней даты. Если получ. число больше 30 - закрываем счет.
<br>Таблица с последней датой по каждому счету<br>
![Screenshot_8](https://user-images.githubusercontent.com/113181404/189384110-7914ef70-fa01-4f49-9d1f-b64fdfd66ccc.png)
<br>Результат<br>
![Screenshot_6](https://user-images.githubusercontent.com/113181404/189383839-2485f5c2-4f57-4876-b816-73b0401c5e46.png)
     
## 11.











