## Лобанчиков Леонид Дмитриевич
## Ссылка на весь код - 

## Весь код с 
create table tarifs(
	ID int(10) primary key,
	NAME VARCHAR(100),
	COST DECIMAL(10.2)
	);
create table clients(
	ID int(10) primary key,
	NAME VARCHAR(1000),
	PLACE_OF_BIRTH VARCHAR(1000),
	DATE_OF_BIRTH date,
	ADDRESS VARCHAR(1000),
	PASSPORT VARCHAR(1000)
	);
create table productype(
	ID int(10) primary key,
	NAME VARCHAR(100),
	BEGIN_DATE date,
	END_DATE date,
	TARIF_REF int(10),
	FOREIGN KEY (TARIF_REF) REFERENCES tarifs(ID)
	);
CREATE table products(
	ID int(10) primary key,
	PRODUCT_TYPE_ID int(10),
	foreign key (PRODUCT_TYPE_ID)  REFERENCES productype(ID),
	name VARCHAR(100),
	CLIENT_REF int(10),
	foreign key (CLIENT_REF) REFERENCES clients(ID),
	OPEN_DATE date,
	CLOSE_DATE date
);

CREATE table accounts(
	ID int(10) primary key,
	NAME VARCHAR(100),
	SALDO decimal(10,2),
	CLIENT_REF int(10),
	foreign key (CLIENT_REF) REFERENCES clients(ID),
	OPEN_DATE date,
	CLOSE_DATE date,
	PRODUCT_REF int(10),
	foreign key (PRODUCT_REF) REFERENCES  products(PRODUCT_TYPE_ID),
	ACC_NUM VARCHAR(25) 
	);
CREATE table records(
	ID int(10) primary key,
	DT int(1),
	SUM DECIMAL(10,2),
	ACC_REF int(20),
	foreign key (ACC_REF) REFERENCES accounts(ID),
	OPER_DATE date
);
insert into tarifs values (1,'Тариф за выдачу кредита', 10);
insert into tarifs values (2,'Тариф за открытие счета', 10);
insert into tarifs values (3,'Тариф за обслуживание карты', 10);
  
insert into clients values (1, 'Сидоров Иван Петрович', 'Россия, Московская облать, г. Пушкин', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать, г. Пушкин, ул. Грибоедова, д. 5', '2222 555555, выдан ОВД г. Пушкин, 10.01.2015');
insert into clients values (2, 'Иванов Петр Сидорович', 'Россия, Московская облать, г. Клин', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать, г. Клин, ул. Мясникова, д. 3', '4444 666666, выдан ОВД г. Клин, 10.01.2015');
insert into clients values (3, 'Агат Сиодр Иванович', 'Россия, Московская облать, г. ВВВ', STR_TO_DATE('01/01/2001','%d/%m/%Y'), 'Россия, Московская облать, г. Балашиха, ул. Пушкина, д. 7', '4444 662326, выдан ОВД г. Клин, 10.01.2015');

insert into productype values (1, 'КРЕДИТ', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 1);
insert into productype values (2,  'ДЕПОЗИТ', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 2);
insert into productype values (3,  'КАРТА', STR_TO_DATE('01/01/2018','%d/%m/%Y'), null, 3);

insert into products values (1, 1, 'Кредитный договор с Сидоровым И.П.', 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'), null);
insert into products values (2, 2, 'Депозитный договор с Ивановым П.С.', 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null);
insert into products values (3, 3, 'Карточный договор с Петровым С.И.', 3, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null);
insert into products values (5, 1, 'Кредитный договор с Петровым С.И.', 3, STR_TO_DATE('01.08.2022','%d.%m.%Y'), STR_TO_DATE('05.09.2022','%d.%m.%Y'));
insert into products values (4, 1, 'Кредитный договор с Сидоровым И.П.', 1, STR_TO_DATE('05.09.2022','%d.%m.%Y'), null);

insert into accounts values (1, 'Кредитный счет для Сидоровым И.П.', -2000, 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'), null, 1, '45502810401020000022');
insert into accounts values (2, 'Депозитный счет для Ивановым П.С.', 6000, 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null, 2, '42301810400000000001');
insert into accounts values (3, 'Карточный счет для Петровым С.И.', 8000, 3, STR_TO_DATE('01.08.2017','%d.%m.%Y'), null, 3, '40817810700000000001');
insert into accounts values (4, 'Кредитный счет для Ивановым П.С.', -22000, 2, STR_TO_DATE('02.08.2017','%d.%m.%Y'), null, 1, '42301810400000000023');
insert into accounts values (5, 'Депозитный счет для Петровым С.И.', 12000, 3, STR_TO_DATE('02.08.2017','%d.%m.%Y'), null, 2, '40817810700000000024');
insert into records values (1, 1, 5000, 1, STR_TO_DATE('01.06.2015','%d.%m.%Y'));
insert into records values (2, 0, 1000, 1, STR_TO_DATE('01.07.2015','%d.%m.%Y'));
insert into records values (3, 0, 2000, 1, STR_TO_DATE('01.08.2015','%d.%m.%Y'));
insert into records values (4, 0, 3000, 1, STR_TO_DATE('01.09.2015','%d.%m.%Y'));
insert into records values (5, 1, 5000, 1, STR_TO_DATE('01.10.2015','%d.%m.%Y'));

insert into records values (6, 0, 3000, 1, STR_TO_DATE('01.10.2015','%d.%m.%Y'));

insert into records values (7, 0, 10000, 2, STR_TO_DATE('01.08.2017','%d.%m.%Y'));
insert into records values (8, 1, 1000, 2, STR_TO_DATE('05.08.2017','%d.%m.%Y'));
insert into records values (9, 1, 2000, 2, STR_TO_DATE('21.09.2017','%d.%m.%Y'));

insert into records values (10, 1, 5000, 2, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
insert into records values (12, 0, 120000, 3, STR_TO_DATE('08.09.2017','%d.%m.%Y'));
insert into records values (13, 1, 1000, 3, STR_TO_DATE('05.10.2017','%d.%m.%Y'));
insert into records values (11, 0, 6000, 2, STR_TO_DATE('26.11.2017','%d.%m.%Y'));
insert into records values (14, 1, 2000, 3, STR_TO_DATE('21.10.2017','%d.%m.%Y'));
insert into records values (15, 1, 5000, 3, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
insert into records values (16, 0, 3000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
insert into records values (17, 1, 3000, 3, STR_TO_DATE('24.08.2022','%d.%m.%Y'));
insert into records values (18, 1, 5000, 4, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
insert into records values (19, 0, 5000, 5, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
insert into records values (20, 0, 2000, 4, STR_TO_DATE('24.10.2017','%d.%m.%Y'));
insert into records values (21, 1, 1000, 5, STR_TO_DATE('24.10.2017','%d.%m.%Y'));

insert into records values (22, 0, 11000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
insert into records values (23, 0, 12000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
insert into records values (24, 0, 13000, 2, STR_TO_DATE('01.09.2022','%d.%m.%Y'));
insert into records values (25, 0, 4000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
insert into records values (26, 0, 5000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
insert into records values (27, 0, 3000, 3, STR_TO_DATE('2.09.2022','%d.%m.%Y'));
insert into records values (28, 0, 1000, 3, STR_TO_DATE('1.09.2022','%d.%m.%Y'));
<br>
***
<br>
# 1.
