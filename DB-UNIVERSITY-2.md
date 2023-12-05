# GROUP

1. Contare quanti iscritti ci sono stati ogni anno

   - SELECT COUNT(\*) , YEAR(`enrolment_date`) AS `year` FROM `students` GROUP BY `year`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

   - SELECT COUNT(\*), `office_address` AS `ufficio` FROM `teachers` GROUP BY `ufficio`;

3. Calcolare la media dei voti di ogni appello d'esame

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

# JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

   - SELECT `degrees`.`name`, `students`.`name`, `students`.`surname` FROM `degrees` INNER JOIN `students` ON `students`.`degree_id` = `degrees`.`id` WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

   - SELECT \* FROM `degrees` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `department_id` = 7 AND `level` = 'magistrale';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

   - SELECT `courses`.\* , `teachers`.`name`, `teachers`.`surname`, `teachers`.`id` FROM `courses` INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`teacher_id` INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` WHERE `teachers`.`name` = 'Fulvio' AND `teachers`.`surname` = 'Amato';

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

   - SELECT `students`.`surname`, `students`.`surname`, `degrees`.`name` , `departments`.`name` FROM `students` INNER JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ORDER BY `students`.`surname` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

   - SELECT `courses`.`name`, `degrees`.`name`, `teachers`.`name`, `teachers`.`surname` FROM `degrees` INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`teacher_id` INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

   - SELECT DISTINCT `departments`.`name` AS `dipartimento`, `teachers`.`surname`, `teachers`.`name` FROM `departments` INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` WHERE `departments`.`name` LIKE '%Matematica';

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.
