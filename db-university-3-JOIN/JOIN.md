# EX - Query con JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name` AS `corso_di_laurea`  
FROM `students`  
INNER JOIN `degrees`  
ON `students`.`degree_id` = `degrees`.`id`  
WHERE `degrees`.`name` = 'Corso di Laurea in Economia'  
ORDER BY `students`.`surname`; 

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

- SELECT `degrees`.`id`, `degrees`.`name`, `degrees`.`level`, `departments`.`name`
FROM `degrees`
INNER JOIN `departments`  
ON `degrees`.`department_id` = `departments`.`id`  
WHERE `degrees`.`level` = 'magistrale' 
AND `departments`.`name` = 'Dipartimento di Neuroscienze';  

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- SELECT `courses`.`id` AS `courses_id`, `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `teachers`.`id` AS `teachers_id`, `teachers`.`name`, `teachers`.`surname`, `teachers`.`office_address`
FROM `courses`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = 'fulvio'
AND `teachers`.`surname` = 'amato'
ORDER BY `courses_id`;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome

- SELECT `students`.`id` AS `students_id`, `students`.`surname`, `students`.`name`, `degrees`.`name` AS `corso_di_laurea`, `degrees`.`level`, `degrees`.`address`, `departments`.`name` AS `nome_dipartimento`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`
;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- SELECT `degrees`.`id` AS `id_corsi_di_laurea`, `degrees`.`name`, `degrees`.`level`, `courses`.`name` AS `nome_corso`, `courses`.`year`, `courses`.`cfu`, `teachers`.`name`, `teachers`.`surname`
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

- SELECT DISTINCT `teachers`.`id` AS `id_docenti`, `teachers`.`name`, `teachers`.`surname`, `departments`.`name` AS `nome_dipartimento`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teachers`.`surname`
;

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

<!-- TODO: da completare -->

- SELECT `students`.`id` AS `id_studenti`, `students`.`name`, `students`.`surname`, `exam_student`.`vote`
FROM `students`
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
;