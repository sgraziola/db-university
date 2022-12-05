# Query Todo:

- Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;
```

- Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT *
FROM `courses`
WHERE `cfu`> 10;
```

- Selezionare tutti gli studenti che hanno più di 30 anni (3490)

```sql
SELECT *
FROM `students`
WHERE DATEDIFF(NOW(), `date_of_birth`) > (365*30);

/* oppure (3324)*/

SELECT *
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, NOW())>30;
```

- Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql
SELECT *
FROM `courses`
WHERE `period` LIKE "I %"
AND `year` = 1;
```

- Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT *
FROM `exams`
WHERE TIME(`hour`) BETWEEN '14:00:00' AND '23:59:59'
AND `date` = "2020-06-20";
```

- Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT *
FROM `degrees`
WHERE `level`="magistrale";
```

- Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(id) as "Total Departments"
FROM `departments`;
```

- Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT *
FROM `teachers`
WHERE `phone` is NULL;
```
