# Reflection #09: Hive 

#### 1. List the 3 Hive Queries you wrote.

__Query #1:__
INSERT OVERWRITE DIRECTORY '/result/Hive_Query01.out' ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' SELECT 5_zipcode, med_income FROM income_table WHERE med_income < 50000;

__Query #2:__

INSERT OVERWRITE DIRECTORY '/result/Hive_Query02.out/' ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' SELECT Id, 5_zipcode, med_income FROM (SELECT Id, med_income, 5_zipcode, AVG(med_income) OVER() AS avg_income FROM income_table) m WHERE med_income > avg_income ORDER BY med_income;

__Query #3:__

INSERT OVERWRITE DIRECTORY '/result/Hive_Query03.out/' ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' SELECT DISTINCT Id, 5_zipcode, med_income FROM income_table ORDER BY med_income DESC LIMIT 10;

#### 2. What technical errors did you experience? Please list them explicitly and identify how you corrected them.

Honestly, there was no technical difficulty as I am now quite familiar with using Docker, and the instruction was straight forward.

#### 3. What conceptual difficulties did you experience?

I actually did not understand why the limitations exist in HiveQL. Why couldn't they make it easy for everyone to use it like the traditional SQL? Also, I need to spend time on how queries execute in multi-table insert query in multiple map-reduce jobs.

#### 4. How much time did you spend on each part of the assignment?

Query #1: 1 Hr 40 Min
Query #2: About 4 Hrs
Query #3: 50 Min

#### 5. Track your time according to the following items: Gitlab & Git, Docker setup/usage, actual reflection work, etc.

Gitlab & Git: 10 Min
Docker setup/usage: 15 Min
Actual reflection: About 6 Hrs

#### 6. What was the hardest part of this assignment?

The Query #2 was tricky. To be able to calculate the average income across all records, the subquery was needed. I tried so many different versions to make the query work. Hive did not let me use the operator within the WHERE clause, but I really wanted to compare the income versus average income. Whenever the JOIN query was used, I continuously getting error below.
`FAILED: SemanticException Cartesian products are disabled for safety reasons.`
or
`only subquery expressions that are top level conjuncts are allowed`.
Finally, I found out the usage of OVER() clause, which let me take the average of entire column and compare it to each row of the dataset. 

#### 7. What was the easiest part of this assignment?

The easiest part of the assignment is setting up the docker environment, as it is like a nature for all of us.

#### 8. What advice would you give someone doing this assignment in the future?

Knowing exactly what you can do and cannot do in Hive is necessary. Traditional SQL and HiveQL are quite similar, but there were many limitations in HiveQL which I had to think and take different approach to reach my goal.

#### 9. What did you actually learn from doing this assignment? 

I Learned the concept of Hive, how Hive stores data, the similarities and differences between the traditional SQL and Hive query language, Hive's data flow, serialization and deserialization in Hive, and how compiler processes HiveQL. Writing the actual query in HiveQL allowed me to think about every components of the Hive, and how the HiveQL and map-reduce works together to make process faster.

#### 10. Why does what I learned matter both academically and practically?

As I learned from the video, reading, and the reflection, Hive is the infrastructure that big companies like Facebook is using heavily. Learning how to program the map-reduce function in hadoop was a good experience which let me understand the procedure of each job. Now I understand how it works, HiveQL basically allowed me to learn how to write a simple query to operate a huge task in a short time with a big efficiency. This was simple enough in academic environment, but I don't see it any much difference in practical environment.


