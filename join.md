# Query Todo:

- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students`.`name`, `students`.`surname`, `students`.`date_of_birth`, `students`.`fiscal_code`, `students`.`enrolment_date`, `students`.`registration_number`, `students`.`email`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";
```

- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT `degrees`.`name`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`
FROM `degrees`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale" AND `departments`.`name` = "Dipartimento di Neuroscienze";
```

- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `courses`.`website`
FROM `courses`
JOIN `course_teacher`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = "Fulvio" AND `teachers`.`surname`= "Amato";

```

- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT `students`.`surname`, `students`.`name` AS 'nome studente', `students`.`registration_number`, `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS 'nome dipartimento'
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;
```

- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT `degrees`.`name` AS 'Degrees_name', `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `courses`.`name` AS 'corse_name', `teachers`.`name` AS 'teacher_name', `teachers`.`surname`
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`;
```

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`,`teachers`.`phone`, `teachers`.`email`, `teachers`.`office_address`, `teachers`.`office_number`
FROM `teachers`
JOIN `course_teacher`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id`= `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";
```

- BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami

```sql
SELECT `students`.`name` AS "Student Name", `students`.`surname`, `students`.`registration_number`, `courses`.`name` AS "Course Name", COUNT(exam_student.vote) AS "numero_tentativi", MAX(exam_student.vote) AS "Voto max"
FROM `students`
JOIN `exam_student`
ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
GROUP BY COUNT(exam_student.vote)
HAVING COUNT(exam_student.vote) < 18
```
