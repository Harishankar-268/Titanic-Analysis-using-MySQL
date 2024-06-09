
# Titanic Analysis using MySQL

- This project uses My SQL to analyze the dataset of an Titanic. The goal of the project is to answer a set of questions about the impact.

### 1.List the first 10 rows of the dataset.

#### Query:
````sql
select * from titanic limit 10;
select * from titanic order by PassengerId desc limit 10;
````
### 2.Find the number of passengers who survived.
#### Query:
````sql
select count(*) as "Passengers_survived" from titanic where Survived = 1 ;
````
### 3.Find the average age of all passengers.
#### Query:
````sql
select avg(age) from titanic;
````
### 4.Find the number of passengers in each class.
#### Query:
````sql
select Pclass,count(*) as "No.of. passengers" from titanic group by Pclass;
````
### 5.Find the first 10 rows of the dataset sorted by passenger class in descending order.
#### Query:
````sql
select * from titanic order by Pclass desc limit 10;
````
### 6.Find the number of passengers in each class sorted by class in ascending order.
#### Query:
````sql
select Pclass, count(*) from titanic group by Pclass order by Pclass asc;
select Pclass, count(*) from titanic group by Pclass order by count(*) asc;
````
### 7.Find the average fare paid by passengers in each class.
#### Query:
````sql
select Pclass,avg(Fare) as "avg_fare" from titanic group by Pclass;
````
### 8.Find the name of the passenger with the highest fare.
#### Query:
````sql
select name,Fare from titanic where fare = (select max(Fare) from titanic);
select max(Fare) from titanic;
````
### 9.Find the name of the passenger who had the highest age among the survivors.
#### Query:
````sql
select name,age from titanic where age= (select max(age) from titanic where Survived = 1)
and Survived =1;
select max(age) from titanic where Survived = 1;
````
### 10.Find the number of passengers who paid more than the average fare.
#### Query:
````sql
select count(*) as num_passengers from titanic where Fare > (select avg(Fare) from titanic);

select avg(Fare) from titanic;
````
### 11.Find the name of the passenger who had the most parents or children on board.
#### Query:
````sql
select name from titanic where Parch = (select max(Parch) from titanic);--

select max(Parch) from titanic
````
### 12.Find the number of male and female passengers who survived, and order the results by sex in ascending order:
#### Query:
````sql
select Sex,count(*) as num_survived from titanic where Survived = 1
group by Sex 
order by Sex asc;
````
### 13.Find the name, age, and fare of the oldest passenger who survived.
#### Query:
````sql
select name,age,Fare from titanic 
where age = (select max(Age)  from titanic where Survived =1)
and Survived =1;
select max(Age)  from titanic where Survived =1;
````
### 14.Find the name and age of the youngest female passenger who survived in third class.
#### Query:
````sql
select name,age from titanic where Sex = "female" and Pclass = 3 and Survived = 1
and age = (select min(Age) from titanic where Sex = "female" and Pclass = 3 and Survived = 1);
select min(Age) from titanic where Sex = "female" and Pclass = 3 and Survived = 1;
````
### 15.Find Number of male and female passengers.
#### Query:
````sql
select 
sum(case when Sex = "male" then 1 else 0 end) as num_male,
sum(case when Sex = "female" then 1 else 0 end) as num_female 

from titanic;
````
### 16.Select all passengers who traveled in a cabin that was not shared by other passengers.
#### Query:
````sql
select * from titanic where cabin not in 
(select Cabin from titanic group by cabin having count(*) > 1);

select Cabin from titanic group by cabin having count(*) > 1;
````
