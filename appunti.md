INNER JOIN

SELECT `degrees`.`name` AS `nome_dipartimento`, `degrees`.`name` as `nome_corso` 
FROM `departments` 
JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id` ;

<!-- FIXME: NON FUNZIONA -->
SELECT `courses`.`id`, `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`
FROM `courses` 
JOIN `degrees`
ON `courses`. `degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'corso di laurea di infromatica'


SELECT `courses`.`id`, `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `exams`.`date`, `exams`.`hour`, `exams`.`address`, `exams`.`location`
FROM `courses` 
INNER JOIN `exams`
ON `courses`. `id` = `exams`.`course_id`
WHERE `courses`.`id`  = 144


SELECT `departments`.*
FROM `departments`
INNER JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `degrees`.`name` = "corso di laurea in diritto dell'economia";


selezionare tutti i docenti che insegnano nel corso di laurea di lettere

da completare

SELECT `teachers`.`name`, `teachers`.`surname`, `teachers`.`email`, `teachers`.`office_address`
FROM `teachers` 
INNER JOIN `courses`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`id` = `course_teacher`.`course


selzionare il libretto universitario di mirko messina

SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `courses`.`name`, `exams`.`date`, `exam_student`.`vote`
FROM `students`
INNER JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
INNER JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
INNER JOIN `courses`
ON `courses`.`id` = `exams`.`course_id`
WHERE `students`.`name` = 'mirco'
AND `students`.`surname` = 'messina'
AND `exam_student`.`vote` >= 18
ORDER BY `exams`.`date`;


selezionare il voto medio di superamento di esami per ogni corso, con anche i dati del corso di laure asocciato, ordinati per media voto 


collegamento delle tabelle
SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, AVG(`exam_student`.`vote`)
FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `exams`
ON `courses`.`id` = `exams`.`course_id`
INNER JOIN `exam_student`
ON `exams`.`id` = `exam_student`.`exam_id`
collegamento delle tabelle

WHERE `exam_student`.`vote` >= 18
GROUP BY `courses`.`id`
ORDER BY `vote_average` DESC
;


SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `students`.`enrolment_date`
FROM `students`
INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'dipartimento di biologia'
ORDER BY `students`.`enrolment_date` DESC
LIMIT 10
OFFSET 0;

