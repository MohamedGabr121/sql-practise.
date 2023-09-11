## https://www.sql-practice.com
This repository is dedicated to students and professionals who would like to brush up and advance their SQL skills for their careers. I found (https://www.sql-practice.com) educational and the web site user friendly however there wasn’t the complete solution book shared on the web site neither on GitHub. So now you can get the answers with alternative solutions for each question 

The test contains 50 questions and consists of 3 category:

- Easy
- Medium
- Hard

You can use the following Entity Relationship Diagram (ERD) to figure out what data to store, the entities, their attributes and also how entities relate to other entities.

![erd](https://user-images.githubusercontent.com/19313466/211203253-23f70de3-4786-45aa-8d7f-54fb81525415.png)


## Answers


---

### Section1: Easy

---

Questions 1- 17

1. Show first name, last name, and gender of patients who's gender is 'M'

```sql

SELECT first_name,
       last_name,
       gender
FROM patients
WHERE gender = 'M';

```

2. Show first name and last name of patients who does not have allergies. (null)

```sql

select first_name,last_name from patients
where allergies is null
