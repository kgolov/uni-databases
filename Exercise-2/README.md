# Заявки в SQL върху две и повече релации

*Забележка. Базите от данни можете да откриете [тук](../Databases/README.md)*

## I. За базата от данни Movies
```SQL
USE MOVIES;
```

### 1. Напишете заявка, която извежда имената на актьорите мъже, участвали във филма The Usual Suspects.
```SQL
SELECT NAME
FROM MOVIESTAR, STARSIN
WHERE GENDER = 'M' AND NAME = STARNAME and MOVIETITLE = 'The Usual Suspects';
```

### 2. Напишете заявка, която извежда имената на актьорите, участвали във филми от 1995, продуцирани от студио MGM.
```SQL
SELECT STARNAME
FROM MOVIE, STARSIN
WHERE YEAR = 1995 AND STUDIONAME = 'MGM' AND MOVIETITLE = TITLE;
```

### 3. Напишете заявка, която извежда имената на продуцентите, които са продуцирали филми на студио MGM.
```SQL
SELECT DISTINCT NAME
FROM MOVIEEXEC, MOVIE
WHERE STUDIONAME = 'MGM' AND CERT# = PRODUCERC#;
```

### 4. Напишете заявка, която извежда имената на всички филми с дължина, поголяма от дължината на филма Star Wars.
```SQL
SELECT MOV2.TITLE
FROM MOVIE AS MOV1, MOVIE AS MOV2
WHERE MOV1.TITLE = 'Star Wars'
AND MOV2.LENGTH > MOV1.LENGTH;
```

### 5. Напишете заявка, която извежда имената на продуцентите с нетни активи поголеми от тези на Stephen Spielberg.
```SQL
SELECT EXEC2.NAME
FROM MOVIEEXEC AS EXEC1, MOVIEEXEC AS EXEC2
WHERE EXEC1.NAME = 'Stephen Spielberg'
AND EXEC2.NETWORTH > EXEC1.NETWORTH;
```

### 6. Напишете заявка, която извежда имената на всички филми, които са продуцирани от продуценти с нетни активи по-големи от тези на Stephen Spielberg.
```SQL
SELECT TITLE
FROM MOVIE, MOVIEEXEC AS EXEC1, MOVIEEXEC AS EXEC2
WHERE EXEC1.NAME = 'Stephen Spielberg'
AND EXEC2.NETWORTH > EXEC1.NETWORTH
AND PRODUCERC# = EXEC2.CERT#;
```

## II. За базата от данни PC
```SQL
USE PC;
```

### 1. Напишете заявка, която извежда производителя и честотата на лаптопите с размер на диска поне 9 GB.
```SQL
SELECT MAKER, SPEED
FROM LAPTOP AS L, PRODUCT AS P
WHERE P.TYPE = 'laptop'
AND L.MODEL = P.MODEL
AND L.HD > 9;
```

### 2. Напишете заявка, която извежда модел и цена на продуктите, произведени от производител с име B.
```SQL
(SELECT L.MODEL, L.PRICE
  FROM LAPTOP AS L, PRODUCT AS P
  WHERE P.MAKER = 'B' AND L.MODEL = P.MODEL)
UNION
(SELECT PC.MODEL, PC.PRICE
  FROM PC, PRODUCT AS P
  WHERE P.MAKER = 'B' AND PC.MODEL = P.MODEL)
UNION
(SELECT PR.MODEL, PR.PRICE
  FROM PRINTER AS PR, PRODUCT AS P
  WHERE P.MAKER = 'B' AND PR.MODEL = P.MODEL);
```

### 3. Напишете заявка, която извежда производителите, които произвеждат лаптопи, но не произвеждат персонални компютри.
```SQL
(SELECT PRODUCT.MAKER
  FROM PRODUCT, LAPTOP
  WHERE PRODUCT.MODEL = LAPTOP.MODEL)
EXCEPT
(SELECT PRODUCT.MAKER
  FROM PRODUCT, PC
  WHERE PRODUCT.MODEL = PC.MODEL);
```

### 4. Напишете заявка, която извежда размерите на тези дискове, които се предлагат в поне два различни персонални компютъра (два компютъра с различен код).
```SQL
SELECT DISTINCT HD
FROM PC AS P1
WHERE P1.HD = ANY (SELECT HD FROM PC P2
WHERE P1.CODE <> P2.CODE);
```

### 5. Напишете заявка, която извежда двойките модели на персонални компютри, които имат еднаква честота и памет. Двойките трябва да се показват само по веднъж, например само (i, j), но не и (j, i).
```SQL
SELECT P1.MODEL, P2.MODEL
FROM PC P1
JOIN PC P2 ON P1.RAM = P2.RAM AND P1.SPEED = P2.SPEED
WHERE P1.CODE < P2.CODE AND P1.MODEL != P2.MODEL
ORDER BY P1.MODEL, P2.MODEL ASC;
```

### 6. Напишете заявка, която извежда производителите на поне два различни персонални компютъра с честота поне 400.
```SQL
SELECT *
FROM PRODUCT P1
JOIN PC P2 ON P1.MODEL = P2.MODEL
WHERE SPEED >= 400 AND P2.CODE <> ANY (
	SELECT CODE FROM PRODUCT P2 JOIN PC ON P2.MODEL = PC.MODEL
	WHERE P1.MAKER = P2.MAKER);
```

## III. За базата от данни SHIPS
```SQL
USE SHIPS;
```

### 1. Напишете заявка, която извежда името на корабите с водоизместимост над 50000.
```SQL
SELECT NAME
FROM SHIPS JOIN CLASSES ON SHIPS.CLASS = CLASSES.CLASS
WHERE DISPLACEMENT > 50000;
```

### 2. Напишете заявка, която извежда имената, водоизместимостта и броя оръдия на всички кораби, участвали в битката при Guadalcanal.
```SQL
SELECT SHIPS.NAME, CLASSES.DISPLACEMENT, CLASSES.NUMGUNS
FROM SHIPS JOIN CLASSES ON SHIPS.CLASS = CLASSES.CLASS
WHERE SHIPS.NAME =
ANY(SELECT SHIP FROM OUTCOMES WHERE BATTLE = 'Guadalcanal');
```

### 3. Напишете заявка, която извежда имената на тези държави, които имат както бойни кораби, така и бойни крайцери.
```SQL
(SELECT COUNTRY FROM CLASSES WHERE TYPE = 'bb')
INTERSECT
(SELECT COUNTRY FROM CLASSES WHERE TYPE = 'bc');
```

### 4. Напишете заявка, която извежда имената на тези кораби, които са били повредени в една битка, но по-късно са участвали в друга битка.
```SQL

```
