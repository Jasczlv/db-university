1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT \*  
FROM `students`  
INNER JOIN `degrees`  
ON `students` . `degree_id` = `degrees` . `id`  
WHERE `degrees` . `name` = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

SELECT `degrees`.\* , `departments` . `name` AS 'department_name'  
FROM `degrees`  
INNER JOIN `departments`  
ON `departments` . `id` = `degrees` . `department_id`  
WHERE `departments` . `name` = 'Dipartimento di Neuroscienze'  
AND `degrees` . `name` LIKE '%Laurea Magistrale%';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT \*  
FROM `course_teacher`  
INNER JOIN `teachers`  
ON `teachers` . `id` = `course_teacher` . `teacher_id`  
INNER JOIN `courses`  
ON `courses` . `id` = `course_teacher` . `course_id`  
WHERE `teachers` . `name` = 'Fulvio'  
AND `teachers` . `surname` = 'Amato'  
AND `teachers` . `id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students` .\*, `degrees` . `name` as `nome_corso` , `departments` . `name` AS `nome_dipartimento`  
FROM `students`  
INNER JOIN `degrees`  
ON `degrees` . `id` = `students` . `degree_id`  
JOIN `departments`  
ON `departments` . `id` = `degrees` . `department_id`  
ORDER BY `students` . `surname` , `students` . `name`;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT degrees . \*, courses . `name` AS `course_name`, CONCAT(teachers . `name`, ' ', teachers . `surname`) AS `teacher_fullname`  
FROM `degrees`  
INNER JOIN `courses`  
ON `courses` . `degree_id` = `degrees` . `id`  
INNER JOIN `course_teacher`  
ON `courses`.`id` = `course_teacher`.`course_id`  
INNER JOIN `teachers`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

SELECT departments . `name` AS `department_name`, CONCAT(teachers . `name`, ' ', teachers . `surname`) AS `teacher_fullname`  
FROM `departments`  
INNER JOIN `degrees`  
ON degrees . `department_id` = departments . `id`  
INNER JOIN `courses`  
ON courses . `degree_id` = degrees . `id`  
INNER JOIN `course_teacher`  
ON `courses`.`id` = `course_teacher`.`course_id`  
INNER JOIN `teachers`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`  
WHERE departments . `name` LIKE 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.
