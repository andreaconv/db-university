# EX - Query con SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)
  - SELECT * 
  - FROM `students` 
  - WHERE YEAR(`date_of_birth`) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
  - SELECT * 
  - FROM `courses` 
  - WHERE `cfu` > 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni
  - SELECT * 
  - FROM `students` 
  - WHERE DATEDIFF(NOW(), `date_of_birth`) / 365.25 > 30;
  <!-- FIXME: Alternativa migliore -->
  - WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
  - SELECT * 
  - FROM `courses` 
  - WHERE `period` = 'I semestre'
  - AND `year` = 1;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
  - SELECT * 
  - FROM `exams` 
  - WHERE `date` = '2020-06-20'
  - AND `hour` > '14:00:00';
  <!-- FIXME: Alternativa migliore -->
  - AND HOUR(`hour`) >= 14;

6. Selezionare tutti i corsi di laurea magistrale (38)
  - SELECT * 
  - FROM `degrees`
  - WHERE `level` = 'magistrale';

7. Da quanti dipartimenti è composta l'università? (12)
  - SELECT `name`
  - FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
  - SELECT * 
  - FROM `teachers` 
  - WHERE `phone` IS NULL;

> ### BONUS

## EX - Query con GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
  - SELECT COUNT(*) AS `iscritti`, YEAR(`enrolment_date`) AS `anno`
  - FROM `students`
  - GROUP BY `anno`
  - ORDER BY `anno`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
  - SELECT COUNT(*) AS `elenco_insegnanti`, `office_address` AS `indirizzo`
  - FROM `teachers` 
  - GROUP BY `indirizzo`
  - ORDER BY `indirizzo`;

3. Calcolare la media dei voti di ogni appello d'esame
  - SELECT AVG(`vote`) AS `media_voti`, `exam_id` AS `appello_esame`
  - FROM `exam_student` 
  - GROUP BY `appello_esame`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
  - SELECT COUNT(*) AS `corsi_di_laurea`, `department_id` AS `dipartimenti`
  - FROM `degrees` 
  - GROUP BY `dipartimenti` ;
