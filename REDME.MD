-- Muestra los profesores que enseñan en la carrera con código '001'
SELECT p.nombre                          -- Muestra el nombre del profesor
FROM PROFESOR p                          -- Toma datos de la tabla PROFESOR con alias 'p'
JOIN PROFCAR pc ON p.codprof = pc.codprof -- Une con PROFCAR donde los códigos de profesor coinciden
WHERE pc.codcarr = '001';                -- Filtra por carrera con código '001'



-- Muestra los alumnos matriculados en la carrera de Derecho (código '004')
SELECT a.nombre                          -- Muestra el nombre del alumno
FROM ALUMNO a                            -- Toma datos de la tabla ALUMNO con alias 'a'
JOIN MATRICULA m ON a.codigoest = m.codigoest -- Une con MATRICULA por código de estudiante
WHERE m.codcarr = '004';                 -- Filtra por carrera con código '004'



-- Muestra los profesores asignados a la carrera de Derecho (código '004')
SELECT p.nombre                          -- Muestra el nombre del profesor
FROM PROFESOR p                          -- Toma datos de la tabla PROFESOR con alias 'p'
JOIN PROFCAR pc ON p.codprof = pc.codprof -- Une con PROFCAR por código de profesor
WHERE pc.codcarr = '004';                -- Filtra por carrera con código '004'



-- Repetición: alumnos en Derecho
SELECT a.nombre
FROM ALUMNO a
JOIN MATRICULA m ON a.codigoest = m.codigoest
WHERE m.codcarr = '004';

-- Repetición: profesores en Derecho
SELECT p.nombre
FROM PROFESOR p
JOIN PROFCAR pc ON p.codprof = pc.codprof
WHERE pc.codcarr = '004';



-- Muestra alumnos en Veterinaria (carrera '008') y el valor que pagaron
SELECT a.nombre, m.valorsemestre         -- Muestra nombre del alumno y valor del semestre
FROM MATRICULA m                         -- Toma datos de la tabla MATRICULA con alias 'm'
JOIN ALUMNO a ON m.codigoest = a.codigoest -- Une con ALUMNO por código de estudiante
WHERE m.codcarr = '008';                 -- Filtra por carrera con código '008'



-- Muestra alumnos que tienen como profesor a 'Portacio Cartagena'
SELECT a.nombre                          -- Muestra el nombre del alumno
FROM ALUMNO a                            -- Toma datos de ALUMNO con alias 'a'
JOIN MATRICULA m ON a.codigoest = m.codigoest -- Une con MATRICULA por estudiante
JOIN PROFESOR p ON m.codprof = p.codprof -- Une con PROFESOR por código de profesor
WHERE p.nombre = 'Portacio Cartagena';  -- Filtra por profesor con ese nombre



-- Muestra el valor más alto pagado por semestre
SELECT MAX(valorsemestre) AS valor_mas_alto -- Selecciona el valor máximo del semestre
FROM MATRICULA;                         -- Desde la tabla MATRICULA



-- Muestra el promedio del valor pagado por semestre
SELECT AVG(valorsemestre) AS promedio_semestre -- Calcula el promedio de los valores del semestre
FROM MATRICULA;                         -- Desde la tabla MATRICULA



-- Muestra alumnos cuyos nombres empiezan con 'A' o terminan en 'r'
SELECT nombre                           -- Muestra el nombre del alumno
FROM ALUMNO                             -- Desde la tabla ALUMNO
WHERE nombre LIKE 'A%' OR nombre LIKE '%r'; -- Filtro: nombres que comienzan con A o terminan en r



-- Muestra el total pagado por cada carrera
SELECT c.descripcion, SUM(m.valorsemestre) AS total_pagado -- Muestra nombre de carrera y suma total pagada
FROM MATRICULA m                         -- Toma datos de MATRICULA con alias 'm'
JOIN CARRERA c ON m.codcarr = c.codcarr -- Une con CARRERA por código de carrera
GROUP BY c.descripcion;                 -- Agrupa resultados por descripción de la carrera



-- Muestra alumnos que no están matriculados en ninguna carrera
SELECT a.nombre                          -- Muestra el nombre del alumno
FROM ALUMNO a                            -- Desde la tabla ALUMNO con alias 'a'
WHERE a.codigoest NOT IN (SELECT codigoest FROM MATRICULA); -- Solo los que no aparecen en MATRICULA
