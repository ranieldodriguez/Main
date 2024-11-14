# Task 1: Sum of Costs
Write a SQL statement to calculate the total cost of all items in a `Book` table, where the table has a column named `Cost`.

```sql
SELECT SUM(Cost) AS TotalCost
FROM Book;
```
# Task 2: Create Patient Table
Write a SQL statement to create a `Patient` table with the following columns:
- `first_name` (varchar(20))
- `last_name` (varchar(30))
- `birthdate` (date)
- `patient_id` (int, primary key)

```sql
CREATE TABLE Patient (
    first_name VARCHAR(20),
    last_name VARCHAR(30),
    birthdate DATE,
    patient_id INT PRIMARY KEY
);
```
# Task 3: Create Exam Table
Write a SQL statement to create an `Exam` table with the following columns:
- `exam_id` (int, primary key, auto-increment)
- `exam_date` (date)
- `exam_reason` (varchar(100))
- `patient_id` (int, foreign key referencing `Patient(patient_id)`)

```sql
CREATE TABLE Exam (
    exam_id INT PRIMARY KEY AUTO_INCREMENT,
    exam_date DATE NOT NULL,
    exam_reason VARCHAR(100),
    patient_id INT,
    FOREIGN KEY (patient_id) REFERENCES Patient(patient_id)
);
```
# Task 4: Update Patient Birthdate
Write a SQL statement to update the birthdate of a patient with a specific `patient_id` in the `Patient` table.

```sql
UPDATE Patient
SET birthdate = '1990-01-01'
WHERE patient_id = 1;
```
# Task 5: Delete a Patient Record
Write a SQL statement to delete a patient record from the `Patient` table based on the `patient_id`.

```sql
DELETE FROM Patient
WHERE patient_id = 1;
```
# Task 6: Create a View for Active Patients
Write a SQL statement to create a view named `ActivePatients` that includes `first_name`, `last_name`, and `birthdate` from the `Patient` table, where the patient status is 'active'.

```sql
CREATE VIEW ActivePatients AS
SELECT first_name, last_name, birthdate
FROM Patient
WHERE status = 'active';
```
# Task 7: Aggregate Function for Patient Count
Write a SQL statement to count the total number of patients in the `Patient` table.

```sql
SELECT COUNT(*) AS TotalPatients
FROM Patient;
```
# Task 8: Joining Tables
Write a SQL statement to select all exams along with patient names from the `Exam` and `Patient` tables.

```sql
SELECT e.exam_id, p.first_name, p.last_name, e.exam_date, e.exam_reason
FROM Exam e
JOIN Patient p ON e.patient_id = p.patient_id;
```
# Task 9: Unique Genres from Book Table
Write a SQL statement to retrieve unique genre values from the `Book` table.

```sql
SELECT DISTINCT Genre
FROM Book;
```
# Task 10: Count Books by Year
Write a SQL statement to count how many books are in the `Book` table for each year.

```sql
SELECT Year, COUNT(*) AS BookCount
FROM Book
GROUP BY Year;
```
