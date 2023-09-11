## https://www.sql-practice.com
This repository is dedicated to students and professionals who would like to brush up and advance their SQL skills for their careers. I found (https://www.sql-practice.com) educational and the web site user friendly however there wasn’t the complete solution book shared on the web site neither on GitHub. So now you can get the answers with alternative solutions for each question 

The test contains 53 questions and consists of 3 category:

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
where allergies is null;

```

3. Show first name of patients that start with the letter 'C'

```sql

select first_name from patients
where first_name like 'C%';

```

4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

```sql
select first_name,last_name from patients
where weight between 100 and 120;
```

5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

```sql
UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;
```

6. Show first name and last name concatenated into one column to show their full name.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;
```

7. Show first name, last name, and the full province name of each patient.

```sql
select first_name , last_name ,province_name
from patients,province_names
where patients.province_id = province_names.province_id;
```

8. Show how many patients have a birth_date with 2010 as the birth year.

```sql
select count(*) as total_patients  from patients
where year(birth_date) =2010;
```

9. Show the first_name, last_name, and height of the patient with the greatest height.

```sql
SELECT first_name, last_name, MAX(height) AS height
FROM patients
GROUP BY first_name, last_name
ORDER BY height DESC
LIMIT 1;
```

10. Show all columns for patients who have one of the following patient_ids:
    1,45,534,879,1000

```sql
SELECT *
FROM patients
WHERE patient_id IN (1, 45, 534, 879, 1000);
```

11. Show the total number of admissions

```sql
SELECT COUNT(admissions.patient_id) AS total_number_of_admissions
FROM admissions;
```
12. Show all the columns from admissions where the patient was admitted and discharged on the same day.

```sql
SELECT *
FROM admissions
WHERE admission_date = discharge_date;
```

13. Show the total number of admissions for patient_id 579.

```sql
SELECT patient_id, COUNT(*) AS total_admissions
FROM admissions
WHERE patient_id = 1
GROUP BY patient_id;
```

14. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?

```sql
SELECT DISTINCT(city) AS unique_cities
FROM patients
         JOIN province_names ON patients.province_id = province_names.province_id
WHERE province_names.province_id = 'NS';
```
15. Write a query to find the first_name, last name and birth date of patients who have height more than 160 and weight more than 70

```sql
SELECT first_name, last_name, birth_date
FROM patients
WHERE height > 160
  AND weight > 70;
```

16. Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null

```sql
SELECT first_name, last_name, allergies
FROM patients
WHERE city = 'Hamilton'
  AND allergies IS NOT NULL;
```

17. Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the
    result order in ascending by city.

```sql
select distinct city
from patients
where
  city like 'a%'
  or city like 'e%'
  or city like 'i%'
  or city like 'o%'
  or city like 'u%'
order by city ASC;
```


---

### Section2: Medium

---

Questions 1- 25


1. Show unique birth years from patients and order them by ascending.

```sql
SELECT * FROM patients
SELECT distinct year(birth_date) FROM patients
order by birth_date asc
select  first_name from patients
group by first_name
having count(first_name)=1
SELECT
patient_id,
first_name
FROM patients
WHERE first_name LIKE 's____%s';

```

2.Show unique first names from the patients table which only occurs once in the list.
For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

```sql
select s.patient_id,first_name,last_name from patients s,admissions a 
where a.patient_id=s.patient_id and diagnosis='Dementia'

```

3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

``sql

select (first_name) from patients
order by len(first_name),first_name;

```

4. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.
   Primary diagnosis is stored in the admissions table.

``sql

SELECT 
  SUM(Gender = 'M') as male_count, 
  SUM(Gender = 'F') AS female_count
FROM patients;

```

5. Display every patient's first_name.
   Order the list by the length of each name and then by alphbetically.

```sql

select first_name,last_name,allergies from patients 
where allergies in('Penicillin','Morphine')
order by allergies ,first_name,last_name;

```
6. Show the total amount of male patients and the total amount of female patients in the patients table.
   Display the two results in the same row.

```sql
select patient_id,diagnosis from admissions 
group by 
patient_id,diagnosis 
having count(*)>1;

```

7. Show the total amount of male patients and the total amount of female patients in the patients table.
   Display the two results in the same row.
```sql

SELECT
  city,
  COUNT(*) AS num_patients
FROM patients
GROUP BY city
ORDER BY num_patients DESC, city asc;

```

8. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

```sql

SELECT first_name, last_name, 'Patient' as role FROM patients
    union all
select first_name, last_name, 'Doctor' from doctors;

```

9. Show the city and the total number of patients in the city.
   Order from most to least patients and then by city name ascending.

```sql

select allergies,count(*) as tot from patients
where allergies is not null
group by  allergies
order by tot desc;

```

10. Show first name, last name and role of every person that is either patient or doctor.
    The roles are either "Patient" or "Doctor"

```sql
SELECT first_name,
       last_name,
       birth_date
FROM patients
WHERE year(birth_date) BETWEEN 1970 AND 1979
ORDER BY birth_date ASC;

