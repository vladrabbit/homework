# Домашнее задание к занятию "`Кеширование Redis/memcached`" - `Владлен Зайцев`


---

### Легенда

	Заказчик передал вам файл в формате Excel, в котором сформирован отчёт.

	На основе этого отчёта нужно выполнить следующие задания.


### Задание 1.

	Опишите не менее семи таблиц, из которых состоит база данных:

    	  какие данные хранятся в этих таблицах;
    	  какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

	Приведите решение к следующему виду:

	Сотрудники (

    	  идентификатор, первичный ключ, serial,
          фамилия varchar(50),
          ...
          идентификатор структурного подразделения, внешний ключ, integer).
 
### Решение 1

## Опишите не менее семи таблиц, из которых состоит база данных:

# какие данные хранятся в этих таблицах;

	1. ФИО сотрудника, Дата найма
	2. Оклад
	3. Должность
	4. Тип подразделения 
	5. Структурное подразделение
	6. Адрес филиала
	7. Проект на который назначен

# какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

	1. [varchar(n), date]
	2. money
	3. varchar(n)
	4. varchar(n)
	5. varchar(n)
        6. varchar(n)
	7. varchar(n)

## Приведите решение к следующему виду:

# Сотрудники

	1: Employee_table

	   emloyee_id = (int)
	   имя = (varchar(50))
           фамилия = (varchar(50))
           отчество = (varchar(50))
           дата найма = (date)
           PRIMARY KEY(pk_employee) = [id, имя, фамилия, отчество, дата приема]
	   FOREIGN KEY = [pk_posotion, pk_structural, pk_address]  

	2: Salary_Table
	   salary_id = (int)
           оклад = (money/float)
	   PRIMARY KEY(pk_salary) = [id, оклад]
           FOREIGN KEY = [emloyee_id]

        3: Position_table
	   position_id = (int)
	   должность = (varchar(50))
           PRIMARY KEY(pk_posotion) = [id, должность]

        4: Type_of_division_table
           type_id = (int)
	   тип подразделения = (varchar(50))
	   PRIMARY KEY(pk_type) = [id, тип подразделения]

	5: Structural_division_table
	   structural_id = (int)
           структурное подразделение = (varchar(50))
           PRIMARY KEY(pk_structural) = [id, структурное подразделение]
	   FOREIGN KEY = [type_id]

	6: Branch_address_table
           branch_id = (int)
           адрес филиала = (varchar(100))
           PRIMARY KEY(pk_address) = [id, адрес филиала]

	7: Project_table
           project_id = (int)
           проект = (varchar(100))
           PRIMARY KEY(pk_project) = [id, проект]
           FOREIGN KEY = [structural_id(1), structural_id(2), structural_id(n)]


---
