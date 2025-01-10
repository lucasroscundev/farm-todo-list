# Steps to set up FastAPI backend
Considering you're inside the backend folder of your project

## Creating virtual environment
```
    python -m venv venv
```
(You can name your virtual environment however you like, but venv is one of the standards.
Replace the second venv for whichever name you prefer.)

## Activate virtual environment
```
    source venv/bin/activate
```

## Installing required packages (Virtual Environment Active)
```
    pip install "fastapi[all]" "motor[srv]" beanie aiostream
```
Motor is an asynchronous mongodb driver for python.
Beanie is an object-document mapper for mongodb, built on top of motor. Allows us to define our data models as python classes, and provides an intuitive api for database operations.
Aiostream provides tools for working with asynchronous streams, which can be useful when dealing with large datasets or real-time data.

## Generate the requirements.txt file
```
    pip freeze > requirements.txt
```
In case installing packages is needed in a different computer
```
    pip install -r requirements.txt
```

## Configuring the Dockerfile
```
FROM python:3

WORKDIR /usr/src/app
COPY requirements.txt ./

RUN pip install --no-cache-dir --upgrade -r ./requirements.txt

EXPOSE 3001

CMD [ "python", "./src/server.py" ]
```
Official Base Image for Python 3, which gives a preconfigured environment with Python installed.
Workdir sets the working directory inside the container.
Copies requirements.txt from local machine to container.
Runs pip install to get all packages needed.
Expose #portnumber informs docker the container will be listed on #portnumber.
CMD runs command that will be executed when the container is started (runs server.py).

## Setting up pyproject.toml
This file is meant to hold information and configurations regarding python in the project.
It is becoming standard practice, and in this case, we are configuring pytest options.
For more info, check https://packaging.python.org/en/latest/guides/writing-pyproject-toml/

## Creating src folder, and basic files
1. Create src folder 
2. Move inside src folder
3. Create server.py, and dal.py
The file dal.py represents data access layer, it is responsible for handling all interactions between application and database. It abstracts the complexities of the operations from the rest of the application.

## The dal.py file
First , we create the models for our mongodb database, as well as for the application, as python classes.
Second, we add methods to our data access layer class, which tells our database what kind of operations we will perform.
All methods area asynchronous(async + await), for non-blocking database operations.
There is extensive use of type hints for better code clarity and IDE support.
Mongodb operations such as find, find one and update, and delete are used.
There is a data transformation, with the conversion between mongodb documents and pydantic models for type safety.
All methods accept a session parameter for transaction support. (Not implemented yet, but this signals at a security feature. Think about authorization and authentication)

## The server.py file
Imports apart, as you can see in the file itsefl, we begin the file defining some variables, such as collection name, database URI(mongodb location, pulled from .env file) and debug.
As a second step, we implement a function to manage the lifecycle for our application, so it does not stay on indefinitely.
The third part is the creation of the FastAPI application using lifespan function defined earlier and using the debug defined at the very beginning.
A fourth section is the creation of the routes(or API endpoints) and their response structures. In this section, we use the classes and functions created at our dal.py file, as if it were our domain. GET, POST, PATCH, DELETE. We've implemented a dummy endpoint for testing. Our main function at the end runs the FastAPI function using uvicorn. FastAPI parses JSON into pydantic models(e.g. NewItem) and automatically creates Swagger documentation for the API.

