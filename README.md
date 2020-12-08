# Bare Bone Simple Python Docker App #  



## Build Docker images  

> docker build -t addemp . -f Dockerfile-AddEmp   
>
> docker build -t getemp . -f Dockerfile-GetEmp 



## Get MySQL Docker Image  

> docker pull mysql



## Create DB and tables  

### Run database container - Making mysql available  

> docker run -d -e MYSQL_ROOT_PASSWORD=abcd1234 --name empdb --net awsecs -p 3306:3306 -v /tmp/mysql-db-store/:/var/lib/mysql mysql:latest
>


### Create database and tables  

> docker container exec -it empdb /bin/bash
>

>> :/# mysql -u root -p
>>
>> :/# mysql>  create database awsecs;
>>
>> :/# mysql> show databases;
>>
>> :/# mysql> use awsecs;
>>
>> :/# mysql> create table Employee (emp_id integer, first_name varchar(40), last_name varchar(40), primary_skills varchar(20), location char(10) );
>>
>> :/# mysql> describe Employee;
>>


## Create application containers  

> docker run -d -e DBHOST="empdb" -e DBPORT="3306" -e DBUSER="root" -e DBPWD="abcd1234" -e DATABASE="awsecs" --name addemp --net awsecs -p 80:80 addemp:latest
>
> docker run -d -e DBHOST="empdb" -e DBPORT="3306" -e DBUSER="root" -e DBPWD="abcd1234" -e DATABASE="awsecs" -name addemp --net awsecs -p 8080:8080 getemp:latest



## Run app  

On browser:
http://localhost:80