# JOIN
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
    SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name`
    FROM `degrees`
    JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
    WHERE `degrees`.`name` = "Corso di Laurea in Economia";

2. Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze
    SELECT `degrees`.*, `departments`.`name` AS `department_name`
    FROM `degrees`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name` = "Dipartimento di Neuroscienze";

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    SELECT `courses`.`name` AS `course_name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
    FROM `teachers`
    JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
    WHERE `teachers`.`id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
    SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`, `students`.`registration_number`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `departments`.`name` AS `departments_name`
    FROM `students`
    JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    ORDER BY `students`.`surname`, `students`.`name` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
    SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
    FROM `course_teacher`
    JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
    SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`phone` AS `teacher_phone`, `teachers`.`email` AS `teacher_email`, `departments`.`name` AS `department_name`
    FROM `teachers`
    JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name` = "Dipartimento di Matematica";

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
    SELECT COUNT(`students`.`id`) AS `exams_number`, `students`.`surname`
    FROM `exam_student`
    JOIN `students` ON `students`.`id` = `exam_student`.`student_id`
    GROUP BY `students`.`surname`