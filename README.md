# Trivia API Guide

## Description

Trivia API is a full-stack application allowing users to play trivia quizzes. Users can browse questions, add new questions, delete questions, and search for questions based on search terms. The backend is built with Flask, and the frontend is built with React.

## Table of Contents

1. Installation
2. Set up and Populate the Database
3. Environment Variables
4. Running the Backend Server
5. Running the Frontend Server
6. API Documentation
7. Testing

## Installation

### Backend Dependencies

1. **Create a Virtual Environment:**

   ```
   python -m venv venv
   ```

2. **Activate the Virtual Environment:**

   - On Windows (CMD):

     ```
     venv\Scripts\activate
     ```

   - On Windows (Git Bash):

     ```
     source venv/Scripts/activate
     ```

   - On macOS/Linux:

     ```
     source venv/bin/activate
     ```

3. **Navigate to the Backend Directory:**

   ```
   cd backend
   ```

4. **Install Dependencies:**
   ```
   pip install -r requirements.txt
   ```

### Frontend Dependencies

1. **Navigate to the Frontend Directory:**

   ```
   cd frontend
   ```

2. **Install Dependencies:**

   ```
   npm install
   ```

## Set up and Populate the Database
Make sure that Postgres is running with:
```
pg_ctl -D "C:\Program Files\PostgreSQL\16\data" start
```
then connect to the database using:
```
psql -U [user]
```
create a trivia database:
```
CREATE DATABASE trivia;
```
From the backend folder in terminal, Populate the database using the trivia.psql file provided. run (cmd):
```
psql trivia [user] < trivia.psql
```
## Environment Variables

Set the following environment variables to configure access to your PostgreSQL database.

1. **Windows (CMD):**

   ```
   set DATABASE_USER=your_postgres_user
   set DATABASE_PASSWORD=your_postgres_password
   set DATABASE_NAME=trivia
   set DATABASE_HOST=localhost
   set DATABASE_PORT=5432
   set FLASK_APP=flaskr
   set FLASK_ENV=development
   ```

2. **Windows (Git Bash), macOS, Linux:**

   ```
   export DATABASE_USER=your_postgres_user
   export DATABASE_PASSWORD=your_postgres_password
   export DATABASE_NAME=trivia
   export DATABASE_HOST=localhost
   export DATABASE_PORT=5432
   export FLASK_APP=flaskr
   export FLASK_ENV=development
   ```

## Running the Backend Server

1. **Ensure the Virtual Environment is Activated:**

   ```
   source venv/Scripts/activate
   ```

2. **Run the Server:**

   ```
   python run.py
   ```

3. **Alternatively, You Can Use Flask:**
   ```
   flask run
   ```
   If you are using GitBash and getting module not found error try:
   ```
   venv/Scripts/python.exe -m flask run
   ```

## Running the Frontend Server

1. **Navigate to the Frontend Directory:**

   ```
   cd frontend
   ```

2. **Start the Frontend Server:**

   ```
   npm start
   ```

## API Documentation

### GET /categories

- **Description**: Fetches all available categories.
- **Request Parameters**: None
- **Response Body**:

  ```
  {
    "success": true,
    "categories": {
      "1": "Science",
      "2": "Art",
      "3": "Geography",
      "4": "History",
      "5": "Entertainment",
      "6": "Sports"
    }
  }
  ```

### GET /questions?page=${integer}

- **Description**: Fetches a paginated set of questions.
- **Request Parameters**:
  - `page` (optional): The page number to fetch.
- **Response Body**:

  ```
  {
    "success": true,
    "questions": [
      {
        "id": 1,
        "question": "This is a question",
        "answer": "This is an answer",
        "difficulty": 5,
        "category": 2
      }
    ],
    "total_questions": 100,
    "categories": {
      "1": "Science",
      "2": "Art",
      "3": "Geography",
      "4": "History",
      "5": "Entertainment",
      "6": "Sports"
    },
    "current_category": null
  }
  ```

### GET /categories/${id}/questions

- **Description**: Fetches questions for a specified category.
- **Request Parameters**:
  - `id` (integer): The ID of the category.
- **Response Body**:

  ```
  {
    "success": true,
    "questions": [
      {
        "id": 1,
        "question": "This is a question",
        "answer": "This is an answer",
        "difficulty": 5,
        "category": 4
      }
    ],
    "total_questions": 100,
    "current_category": "History"
  }
  ```

### DELETE /questions/${id}

- **Description**: Deletes a specified question.
- **Request Parameters**:
  - `id` (integer): The ID of the question.
- **Response Body**:

  ```
  {
    "success": true,
    "deleted": 1
  }
  ```

### POST /questions

- **Description**: Adds a new question.
- **Request Body**:

  ```
  {
    "question": "Here's a new question string",
    "answer": "Here's a new answer string",
    "difficulty": 1,
    "category": 3
  }
  ```

- **Response Body**:

  ```
  {
    "success": true,
    "created": 1
  }
  ```

### POST /questions/search

- **Description**: Searches for questions by search term.
- **Request Body**:

  ```
  {
    "searchTerm": "this is the term the user is looking for"
  }
  ```

- **Response Body**:

  ```
  {
    "success": true,
    "questions": [
      {
        "id": 1,
        "question": "This is a question",
        "answer": "This is an answer",
        "difficulty": 5,
        "category": 5
      }
    ],
    "total_questions": 100,
    "current_category": "all"
  }
  ```

### POST /quizzes

- **Description**: Fetches the next quiz question.
- **Request Body**:

  ```
  {
    "previous_questions": [1, 4, 20, 15],
    "quiz_category": {
      "type": "current category",
      "id": 1
    }
  }
  ```

- **Response Body**:

  ```
  {
    "success": true,
    "question": {
      "id": 1,
      "question": "This is a question",
      "answer": "This is an answer",
      "difficulty": 5,
      "category": 4
    }
  }
  ```

## Testing

If you are working in a local environment, you'll need to manually set up and populate the testing database:

To deploy the tests, run
```
dropdb trivia_test

createdb trivia_test

psql trivia_test < trivia.psql
```

To run the tests, execute:

```
python test_flaskr.py
```
