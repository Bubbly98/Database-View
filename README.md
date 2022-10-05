# Database-View

Questions 01
Create a view named student_names to store student registration number, firstname and surname.

Question 02
Create a view named new_students to store registration number and first name of the students whose
registration number is greater than 55555.

Question 03
Create a view to store the details of students who are registered to EED001 after 2011. Display student
name, registration number and registration year.

Question 04
Create a view named number_of_students_for_subject to view subject code, title and number of
students for each subject.

Question 05
Create a view to show the student details who did not attended to the lab classes.

Question 06
Create a view to display all the student registration numbers of students who are registered after 2012.

Question 07
Create a view to store all the subject codes and number of class hall which are allocated for
each
subject.

Question 08
Using student_names view change Peter’s surname to Willson.

----------------------------ANSWERS---------------------------------------------

DROP DATABASE LABTEST2;
 

CREATE DATABASE LABTEST2;
  USE LABTEST2;

  CREATE TABLE SUBJECT(
     S_CODE VARCHAR(255) NOT NULL PRIMARY KEY,
     S_TITLE VARCHAR(255) NOT NULL,
     No_of_students VARCHAR (10) NOT NULL);


  DESC SUBJECT;

  INSERT INTO SUBJECT(s_code,s_title,No_of_students)
     VALUES
     ('EED001','DATA STRUCTURES','50'),
     ('EEX4366','DATA MODELLING','150'),
     ('MHZ4259','STATISTICS','45'),
     ('MHZ4379','MATHS','20'),
     ('EEI3372','PYTHON','23'),
     ('EEI4362','JAVA','100');

    SELECT*FROM SUBJECT;

    CREATE TABLE STUDENT(
    
     s_reg varchar(255) NOT NULL PRIMARY KEY,
     s_fname varchar(255) NOT NULL,
     s_sname varchar(255),
     tel_no int ,
     address varchar(255)
     );

    DESC STUDENT;

    INSERT INTO STUDENT(s_reg,s_fname,s_sname,tel_no,address)
     VALUES
     ('55556','ANURADHA','NANDASENA','0764571389','COLOMBO'),
     ('02','NAWODA','NANDASENA','0764571389','BALANGODA'),
     ('03','AKILA','LIYANAGE','0764571389','GALLE');

    SELECT * FROM STUDENT;

    CREATE TABLE STUDENT_SUBJECT(
     s_reg VARCHAR(255) NOT NULL,
     s_code varchar(255) NOT NULL,
     year_reg DATE,
     CONSTRAINT FK_STUDENTSTUDENT_SUBJECT FOREIGN KEY(s_reg) REFERENCES STUDENT(s_reg),
     CONSTRAINT FK_SUBJECTSTUDENT_SUBJECT FOREIGN KEY(s_code) REFERENCES SUBJECT(s_code)
     );

    DESC STUDENT_SUBJECT;

    INSERT INTO STUDENT_SUBJECT(s_reg,s_code,year_reg)
     VALUES
     ('01','EEX4366','2020.08.28');

     CREATE TABLE CLASS_SHEDULE(
    
     s_code varchar(255) NOT NULL,
     classhall varchar(255) NOT NULL,
     classdate DATE NOT NULL,
     day VARCHAR(255),
     time TIME,
     CONSTRAINT FK_SUBJECTCLASS_SHEDULE FOREIGN KEY(s_code) REFERENCES SUBJECT(s_code)
     );

     DESC CLASS_SHEDULE;

     INSERT INTO CLASS_SHEDULE(s_code,classhall,classdate,day,time)
     VALUES('EEX4366','HALL-1','2022.06.15','SUNDAY','11.30.00'),
             ('EEI4362','HALL-1','2022.06.14','SATURDAY','3.00.00');

    SELECT  * FROM CLASS_SHEDULE;
    
     CREATE TABLE CLASSATTENDENCE(
    
     s_reg VARCHAR(255) NOT NULL,
     s_code varchar(255) NOT NULL,
     classdate DATE NOT NULL,
     classhall varchar(255) NOT NULL,
     attendence varchar(255),
     CONSTRAINT FK_STUDENTCLASSATTENDENCE FOREIGN KEY(s_reg) REFERENCES STUDENT(s_reg),
     CONSTRAINT FK_SUBJECTCLASSATTENDENCE FOREIGN KEY(s_code) REFERENCES SUBJECT(s_code)
     );

    DESC CLASSATTENDENCE;

    INSERT INTO CLASSATTENDENCE(s_reg,s_code,classdate,classhall,attendence)
     VALUES
     ('55556','EEX4366','2022.06.15','HALL-1','YES');

    SELECT * FROM CLASSATTENDENCE;




Q1)
CREATE VIEW Student_Names AS 
SELECT s_reg,s_fname,s_sname
FROM STUDENT;

SELECT * FROM Student_Names;

Q2)
CREATE VIEW New_Students AS 
SELECT s_reg,s_fname
FROM STUDENT
WHERE s_reg>55555;


SELECT * FROM New_Students;


Q3)
CREATE VIEW Store_Details AS 
SELECT STUDENT.s_sname,STUDENT_SUBJECT.s_reg,STUDENT_SUBJECT.year_reg
FROM STUDENT,STUDENT_SUBJECT
WHERE STUDENT_SUBJECT.s_code='EED001' AND STUDENT_SUBJECT.year_reg >'2011';

SELECT * FROM Store_Details;

Q4)
CREATE VIEW Number_of_students_for_subject AS 
SELECT s_code,s_title,No_of_students
FROM SUBJECT;



Q5)
CREATE VIEW Show_Student_Details AS 
SELECT STUDENT.s_sname,CLASSATTENDENCE.s_reg,CLASSATTENDENCE.s_code
FROM STUDENT,CLASSATTENDENCE
WHERE CLASSATTENDENCE.attendence='NO';

SELECT * FROM Show_Student_Details;

Q6)
CREATE VIEW Display_After_2012 AS 
SELECT year_reg
FROM STUDENT_SUBJECT
WHERE year_reg > '2012';

SELECT * FROM Display_After_2012;

Q7)
CREATE VIEW Display_Class_Halls AS 
SELECT s_code,classhall
FROM CLASS_SHEDULE;

SELECT * FROM Display_Class_Halls;

Q8)
UPDATE Student_Names
SET s_fname = 'Peter'
WHERE s_reg = '02';

UPDATE Student_Names
SET s_sname = 'Wilson'
WHERE s_reg = '02';
SELECT * FROM Student_Names;
