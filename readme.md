# AWS 2 Tier Architecture Project

##### This is a Flask Based Docker application which interects with Amazon Aurora Serverless using Data API

It has 2 endpoints: 
- Create Person
- Get Person

### 1. Creating Aurora Instance 
We create an RDS Aurora instance with Postgres compatibilty and setup the credentials for it.

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/1.JPG "Aurora")

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/2.JPG "Aurora")

------------
### 2. Storing Aurora Credentials in Secrets Manager
It is a good practise to store our credentials in Secrets Manager. We need to note down the Secret ARN id which will be used in our Flask Application Code.
![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/3.JPG "Aurora")
![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/4.JPG "Aurora")
------------

### 3. Creating IAM Role to access RDS
We create an RDS role with the following policies so that it could access the Database with the secrets. 

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/5.JPG "Aurora")

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/6.JPG "Aurora")

We need to add the Access Key id and Secret Access Id  in our Application Code.
> Note: In production always use Environment Variable to store the access keys/id in any code. 

------------

### 4. Deploying Docker Container 
We create docker image using our Dockerfile and then create a container out of the generated Image.

Make sure you are in the same directory with the Dockerfile.
To create the docker image:
```shell
docker build -t flask-app .
```
To create docker container:
```
docker run -d --name flask-app -p 8081:8081 flask-app
```
The container will run on http://localhost:8081

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/9.JPG "Aurora")
------------
### 5. Accessing the Table using the Endpoints
A Persons table is already been made using Query Editor on Aurora DB cluster.
We can query the table and add any person details or fetch any details using the endpoint.

We can use POSTMAN to test it.

![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/7.JPG "Aurora")


![Aurora](https://github.com/gunishjain/RDS-ServerLess-Flask-App/blob/main/SS/8.JPG "Aurora")

------------



