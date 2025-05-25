# Домашнее задание к занятию "`Базы данных`" - `Холопко Антон`


---

### Легенда

Заказчик передал вам [файл в формате Excel](https://github.com/netology-code/sdb-homeworks/blob/main/resources/hw-12-1.xlsx), в котором сформирован отчёт. 

На основе этого отчёта нужно выполнить следующие задания.

### Задание 1

Опишите не менее семи таблиц, из которых состоит база данных:

- какие данные хранятся в этих таблицах;
- какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

Приведите решение к следующему виду:

Сотрудники (

- идентификатор, первичный ключ, serial,
- фамилия varchar(50),
- ...
- идентификатор структурного подразделения, внешний ключ, integer).

## Решение

```
Сотрудники (
    id SERIAL PRIMARY KEY,
    фамилия VARCHAR(50),
    имя VARCHAR(50),
    отчество VARCHAR(50),
    дата_найма DATE,
    оклад NUMERIC(10, 2),
    должность_id INTEGER REFERENCES Должности(id),
    подразделение_id INTEGER REFERENCES Подразделения(id)
);
```

```
Подразделения (
    id SERIAL PRIMARY KEY,
    название VARCHAR(100),
    тип_подразделения_id INTEGER REFERENCES Типы_подразделений(id),
    адрес_филиала_id INTEGER REFERENCES Адреса_филиалов(id)
);
```

```
Типы_подразделений (
    id SERIAL PRIMARY KEY,
    тип VARCHAR(50)
);
```

```
Проекты (
    id SERIAL PRIMARY KEY,
    название VARCHAR(200),
    описание TEXT
);
```

```
Адреса_филиалов (
    id SERIAL PRIMARY KEY,
    адрес VARCHAR(200)
);
```

```
Должности (
    id SERIAL PRIMARY KEY,
    название VARCHAR(100),
    уровень VARCHAR(50)
);
```

```
Назначения_на_проекты (
    id SERIAL PRIMARY KEY,
    сотрудник_id INTEGER REFERENCES Сотрудники(id),
    проект_id INTEGER REFERENCES Проекты(id),
    дата_начала DATE,
    дата_окончания DATE
);
```
