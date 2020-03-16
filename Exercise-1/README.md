# Прости заявки в SQL

*Забележка. Базите от данни можете да откриете [тук](../Databases/README.md)*

## I. За базата от данни Movies
```SQL
USE MOVIES;
```

### 1. Напишете заявка, която извежда адреса на студио ‘Disney’
```SQL
SELECT ADDRESS
FROM STUDIO
WHERE NAME = 'Disney';
```

### 2. Напишете заявка, която извежда рождената дата на актьора Jack Nicholson
```SQL
SELECT BIRTHDATE
FROM MOVIESTAR
WHERE NAME = 'Jack Nicholson';
```

### 3. Напишете заявка, която извежда имената на актьорите, които са участвали във филм от 1980 или във филм, в чието заглавие има думата ‘Knight’
```SQL
SELECT STARNAME
FROM STARSIN
WHERE MOVIEYEAR = 1980 OR MOVIETITLE LIKE '%Knight%';
```

### 4. Напишете заявка, която извежда имената на продуцентите с нетни активи над 10 000 000 долара
```SQL
SELECT NAME
FROM MOVIEEXEC
WHERE NETWORTH > 10000000;
```

### 5. Напишете заявка, която извежда имената на актьорите, които са мъже или живеят на Prefect Rd.
```SQL
SELECT NAME
FROM MOVIESTAR
WHERE GENDER = 'M' OR ADDRESS = 'Perfect Rd.';
```

## II. За базата от данни PC
```SQL
USE PC;
```
### 1. Напишете заявка, която извежда модел, честота и размер на диска за всички персонални компютри с цена под 1200 долара. Задайте псевдоними за атрибутите честота и размер на диска, съответно MHz и GB
```SQL
SELECT MODEL, SPEED AS MHZ, HD AS GB
FROM PC
WHERE PRICE < 1200;
```

### 2. Напишете заявка, която извежда производителите на принтери без повторения
```SQL
SELECT DISTINCT MAKER
FROM PRODUCT
WHERE TYPE = 'Printer';
```

### 3. Напишете заявка, която извежда модел, размер на паметта, размер на екран за лаптопите, чиято цена е над 1000 долара
```SQL
SELECT MODEL, RAM, SCREEN
FROM LAPTOP
WHERE PRICE > 1000;
```

### 4. Напишете заявка, която извежда всички цветни принтери
```SQL
SELECT *
FROM PRINTER
WHERE COLOR = 'y';
```

### 5. Напишете заявка, която извежда модел, честота и размер на диска за тези персонални компютри със CD 12x или 16x и цена под 2000 долара.
```SQL
SELECT MODEL, SPEED, HD
FROM PC
WHERE (CD = '12x' OR CD = '16x') AND PRICE < 2000;
```

## III. За базата от данни SHIPS
```SQL
USE SHIPS;
```

### 1. Напишете заявка, която извежда класа и страната за всички класове с помалко от 10 оръдия.
```SQL
SELECT CLASS, COUNTRY
FROM CLASSES
WHERE NUMGUNS < 10;
```

### 2. Напишете заявка, която извежда имената на корабите, пуснати на вода преди 1918. Задайте псевдоним shipName на колоната.
```SQL
SELECT NAME AS SHIPNAME
FROM SHIPS
WHERE LAUNCHED < 1918;
```

### 3. Напишете заявка, която извежда имената на корабите потънали в битка и имената на съответните битки.
```SQL
SELECT SHIP, BATTLE
FROM OUTCOMES
WHERE RESULT = 'sunk';
```

### 4. Напишете заявка, която извежда имената на корабите с име, съвпадащо с името на техния клас.
```SQL
SELECT NAME
FROM SHIPS
WHERE NAME = CLASS;
```

### 5. Напишете заявка, която извежда имената на корабите, които започват с буквата R.
```SQL
SELECT NAME
FROM SHIPS
WHERE NAME LIKE 'R%';
```

### 6. Напишете заявка, която извежда имената на корабите, които съдържат 2 или повече думи.
```SQL
SELECT NAME
FROM SHIPS
WHERE NAME LIKE '% %';
```
