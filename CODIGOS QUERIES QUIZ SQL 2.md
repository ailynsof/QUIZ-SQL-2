CODIGOS QUERIES QUIZ SQL 2

**1.**  

*A.*

SELECT \* FROM tic\_2023--Registros 2023--;

*B.*

SELECT DISTINCT actividad\_nombre FROM tic\_2023 --Tipo de actividad--;

**2.**

SELECT

&#x20;   sede\_codigo     AS codigo\_sede,

&#x20;   actividad\_codigo AS codigo\_actividad,

&#x20;   actividad\_nombre AS nombre\_actividad

FROM tic\_2022

ORDER BY sede\_codigo ASC

LIMIT 50;

**3.**

CREATE TABLE tic\_sedes\_resumen (

&#x20;   resumen\_id        INT,

&#x20;   sede\_codigo       INT,

&#x20;   anio              INT,

&#x20;   total\_actividades INT,

&#x20;   tiene\_internet    BOOLEAN,

&#x20;   fecha\_carga       DATETIME,

&#x20;   UNIQUE (sede\_codigo, anio)

);

**4.**

SELECT

&#x20;   LEFT(sede\_codigo, 2)               AS codigo\_departamento,

&#x20;   COUNT(DISTINCT sede\_codigo)        AS total\_sedes

FROM TIC\_2023

WHERE actividad\_codigo = '05'

GROUP BY LEFT(sede\_codigo, 2)

HAVING COUNT(DISTINCT sede\_codigo) > 500

ORDER BY total\_sedes DESC;

**5.**

SELECT

&#x20;   sede\_codigo                          AS sede\_codigo,

&#x20;   COUNT(total\_act\_2022)                AS total\_act\_2022,

&#x20;   COUNT(total\_act\_2023)                AS total\_act\_2023,

&#x20;   COUNT(total\_act\_2023) - COUNT(total\_act\_2022) AS diferencia,

&#x20;   CASE

&#x20;       WHEN COUNT(total\_act\_2023) - COUNT(total\_act\_2022) > 0 THEN 'INCREMENTO'

&#x20;       WHEN COUNT(total\_act\_2023) - COUNT(total\_act\_2022) < 0 THEN 'DECREMENTO'

&#x20;       ELSE 'SIN CAMBIO'

&#x20;   END AS tendencia

FROM (

&#x20;   SELECT sede\_codigo,

&#x20;          sede\_codigo AS total\_act\_2022,

&#x20;          NULL        AS total\_act\_2023

&#x20;   FROM tic\_2022

&#x20;   UNION ALL

&#x20;   SELECT sede\_codigo,

&#x20;          NULL        AS total\_act\_2022,

&#x20;          sede\_codigo AS total\_act\_2023

&#x20;   FROM tic\_2023

) AS datos

GROUP BY sede\_codigo

HAVING COUNT(total\_act\_2022) >= 2

ORDER BY diferencia DESC

LIMIT 30;

