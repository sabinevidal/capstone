# Text Tutor Application
## Udacity Full Stack Nanodegree - Capstone Project
This application is a tool which allows students and tutors to connect. It is based on the growing need for students to obtain extra support while they are not allowed in school during the COVID-19 pandemic. In South Africa a group who normally facilitate in-person extra tutoring for high-school students from disadvantaged backgrounds have started a text-based tutoring program where tutors are able to help students with their school work over text. This applicaiton aims to (theoreticlly) help this program to match tutors and students. Tutors can create an account where they can create a profile and list what subjects and grades they are able to help with. Students can then create an account where they can access the list of tutors and reach out to one which can help them. 

This is my capstone project for the [Udacity Full Stack Web Developer Nanodegree](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd0044). It is required to demonstrate proficiency in the following areas:

* Data modeling
    * Architect relational database models in Python
    * Utilize SQLAlchemy to conduct database queries
* API Architecture and Testing
    * Follow RESTful principles of API development using Flask
    * Structure endpoints to perform CRUD operations, as well as error handling
    * Demonstrate validity of API behavior using the unittest library
* Third Party Authentication
    * Configure Role Based Authentication and roles-based access control (RBAC) in a Flask application utilizing Auth0
    * Decode and verify JWTs from Authorization headers
* Deployment
    * API is [hosted live via Heroku]()
* Optional
    * Design and create a frontend which works with the API and redirects the user to Auth0 for login.
    * Used React.js for frontend

## Getting Started
### Installing Dependencies

Developers should have Python3, pip3, node, and npm installed.

### Frontend dependencies
#### Installing Node and NPM

This project depends on Nodejs and Node Package Manager (NPM). Find and download Node and npm (which is included) at: [https://nodejs.com/en/download](https://nodejs.org/en/download/).

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```
### Backend Dependencies 

Once you have your virtual environment setup and running, install dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

## Running Your Frontend in Dev Mode

The frontend app was built using create-react-app. In order to run the app in development mode use ```npm start```. You can change the script in the ```package.json``` file. 

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.<br>

```bash
npm start
```

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql text-tutor < text-tutor.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

## Testing
To run the tests, run
```
dropdb texttutor_test
createdb texttutor_test
psql texttutor_test < text-tutor.psql
python test_app.py
```

## API Reference

### Getting Started
#### !!TODO!!
Base URL: Currently this application is only hosted locally. The backend is hosted at http://127.0.0.1:5000/
Authentication: This version does not require authentication or API keys.

### Error Handling

There are four types of errors the API will return`;
- 400 - bad request
- 401 - unauthorised
- 404 - resource not found
- 422 - unprocessable
- 500 - internal server error

## API
In order to use the API users need to be authenticated. Users can either have a athlete or a coach role. An overview of the API can be found below as well. We've also provided a Postman Collection.

### Roles and Permissions

#### Admin

Admin can retrieve and manage all information about tutors and subjects

They have the following permissions:

* get:subjects
* get:all_stats

#### Tutor

Athletes can create an athlete and manage their stats through CRUD operations.

They have the following permissions:

post:athlete
post:stat
patch:stat
delete:stat

#### Student

Students can create an athlete and manage their stats through CRUD operations.

They have the following permissions:

post:athlete
post:stat
patch:stat
delete:stat

### Endpoints

#### GET '/tutors'
- Returns a list of tutors with their details and associated classes.
- Does not require authorisation
- Sample: `curl http://127.0.0.1:5000/api/tutors -X GET -H "Content-Type: application/json"`
```
{
  "success": true,
  "tutors": [
    {
      "classes": [
        {
          "grade": 10,
          "id": 1,
          "name": "English"
        },
        {
          "grade": 7,
          "id": 2,
          "name": "Science"
        }
      ],
      "email": "name@email.com",
      "id": 1,
      "name": "Bob",
      "phone": "12323445364"
    },
    {
      "classes": [
        {
          "grade": 7,
          "id": 2,
          "name": "Science"
        },
        {
          "grade": 9,
          "id": 3,
          "name": "English"
        }
      ],
      "email": "name1@email.com",
      "id": 2,
      "name": "Sally",
      "phone": "12323445366"
    },
    {
      "classes": [
        {
          "grade": 7,
          "id": 2,
          "name": "Science"
        },
        {
          "grade": 9,
          "id": 3,
          "name": "English"
        }
      ],
      "email": "name2@email.com",
      "id": 3,
      "name": "Joe",
      "phone": "237593456"
    }
  ]
}
```
#### GET '/tutors/<int:id>'
- Returns a tutor using URL paramteres to specify its id.
- Requires admin, teacher and student account authorisation
- Sample: `curl http://127.0.0.1:5000/api/tutors/<int:id> -X GET -H 'Authorization: Bearer <INSERT_YOUR_TOKEN>' `
``` 
{
  "success": true,
  "tutor": {
    "classes": [
      {
        "grade": 10,
        "id": 9,
        "name": "English"
      },
      {
        "grade": 8,
        "id": 10,
        "name": "English"
      }
    ],
    "email": "bill@email.com",
    "id": 4,
    "name": "Bill",
    "phone": "12323445364"
  }
}
```

#### GET '/subjects'
- Returns a list of subjects.
- Does not require authorisation
- Sample: `curl http://127.0.0.1:5000/api/subjects `
```
{
  "subjects": [
    {
      "grade": 10,
      "id": 3,
      "name": "Maths"
    },
    {
      "grade": 9,
      "id": 2,
      "name": "English"
    },
    {
      "grade": 8,
      "id": 1,
      "name": "English"
    }
  ],
  "success": true
}
```

#### GET '/subjects/<int:id>'
- Returns a subject using URL paramteres to specify its id.
- Requires admin account authorisation
  - Execute export ADMIN_ROLE_TOKEN=<active_admin_jwt> with active Admin JWT before request.
- Sample: `curl http://127.0.0.1:5000/api/tutors/<int:id> -X GET -H 'Authorization: Bearer <INSERT_YOUR_TOKEN>' `
```
{
  "subject": {
    "grade": 8,
    "id": 1,
    "name": "English"
  },
  "success": true
}
```

#### POST '/tutors'
- Creates a new tutor using JSON request parameters in the database
- Requires admin and tutor account authorisation
- Sample: `curl http://127.0.0.1:5000/api/tutors -X POST -H "Content-Type: application/json" -d '{"classes": [{"grade": 10,"id": 4,"name":"English"},{"grade": 8,"id": 7,"name": "English"}],"email": "bill@email.com","name": "Bill","phone": "12323445364"}'`
- Created tutor:
```
{
  "email": "bill@email.com",
  "name": "Bill",
  "phone": "12323445364",
  "classes": [
    {
      "grade": 10,
      "id": 4,
	    "name": "English"
    },
    {
      "grade": 8,
      "id": 7,
	    "name": "English"
    }
  ]
}
```
- JSON response:
```
{
  "success": true,
  "tutor": {
    "classes": [
      {
        "grade": 10,
        "id": 9,
        "name": "English"
      },
      {
        "grade": 8,
        "id": 10,
        "name": "English"
      }
    ],
    "email": "bill@email.com",
    "id": 4,
    "name": "Bill",
    "phone": "12323445364"
  }
}
```

#### POST '/subjects'
- Creates a new subject using JSON request parameters in the database
- Requires admin and tutor account authorisation
- Sample: `curl http://127.0.0.1:5000/api/subjects -X POST -H "Content-Type: application/json" -d '{"name": "English", "grade": "8"}'`
- Created subject:
```
{
  "grade": 8,
  "name": "English"
}
```
- JSON response:
```
{
  "subject": {
    "grade": 8,
    "id": 13,
    "name": "English"
  },
  "success": true
}
```


#### PATCH '/tutors/<int:id>'
- Updates an existing tutor profile using URL parameters specifying tutor id.
- Requires admin and tutor account authorisation
  - Using active Public or Admin JWT before request, execute
    export PUBLIC_ROLE_TOKEN=<active_public_jwt>
    or
    export ADMIN_ROLE_TOKEN=<active_admin_jwt>
- Sample: `curl http://127.0.0.1:5000/api/tutors/1 -X PATCH -H 'Authorization: Bearer <INSERT_YOUR_TOKEN>' -H 'Content-Type: application/json' -d '{"email":"patch@email.com", "classes": [{"grade": 10, "id": 9, "name": "English"}]}'`
```
{
  "success": true,
  "tutors": {
    "classes": [
      {
        "grade": 10,
        "id": 14,
        "name": "English"
      },
      {
        "grade": 8,
        "id": 15,
        "name": "English"
      }
    ],
    "email": "patch@email.com",
    "id": 1,
    "name": "Joe",
    "phone": "237593456"
  }
}
```

#### DELETE '/tutors/<int:id>'
- Deletes an existing tutor profile using URL parameters specifying tutor id.
- Requires admin and tutor account authorisation
  - Using active Public or Admin JWT before request, execute
    export PUBLIC_ROLE_TOKEN=<active_public_jwt>
    or
    export ADMIN_ROLE_TOKEN=<active_admin_jwt>
- Sample: `curl http://127.0.0.1:5000/api/tutors/1 -X DELETE -H 'Authorization: Bearer <INSERT_YOUR_TOKEN>'`
```
{
  "success": true,
  "tutor": "Bob",
  "tutor_id": 1
}
```

#### DELETE '/subjects/<int:id>'
- Deletes an existing subject using URL parameters specifying subject id.
- Requires admin account authorisation
  - Using active Public or Admin JWT before request, execute
    export ADMIN_ROLE_TOKEN=<active_admin_jwt>
- Sample: `curl http://127.0.0.1:5000/api/subjects/1 -X DELETE -H 'Authorization: Bearer <INSERT_YOUR_TOKEN>'`
```

```