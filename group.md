# Query Todo:

- Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(`enrolment_date`) AS "Year", COUNT(id) AS "Subscription per Year"
FROM `students`
GROUP BY YEAR(`enrolment_date`);

```

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT `office_address` AS "Buildings", COUNT(id) AS "Teachers"
FROM `teachers`
GROUP BY `office_address`;
```

- Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT `exam_id` AS "Exam", AVG(`vote`) AS "Average Vote"
FROM `exam_student`
GROUP BY `exam_id`;
```

- Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT `department_id` AS "Department", COUNT(id) AS "Courses"
FROM `degrees`
GROUP BY `department_id`;
```
