# Quiz Setter Question Generator API Documentation

**Base URL**: `https://quiz-setter.onrender.com`

## Overview

The Quiz Setter API allows users to upload PDF files, extract text, and generate multiple-choice questions. It supports various functionalities including retrieving generated questions, submitting answers, and viewing results.

## Table of Contents
1. [Home](#home)
2. [Upload PDF File](#upload-pdf-file)
3. [Retrieve Questions](#retrieve-questions)
4. [Submit Answers](#submit-answers)
5. [Retrieve Results](#retrieve-results)
6. [Error Handling](#error-handling)
7. [Postman Instructions](#postman-instructions)

---

## 1. Home

### Endpoint
```
GET /
```

### Description
Welcome message for the Quiz Setter API.

### Response
```json
{
    "message": "Welcome to Quiz Setter Question Generator API! In association with Qwab."
}
```


## 2. Upload PDF File

### Endpoint
```
POST /upload
```

### Description
Upload a PDF file to extract text and generate multiple-choice questions.

### Request
#### Headers
- `Content-Type`: `multipart/form-data`

#### Body
- **Key**: `pdf`
  - **Type**: `File`
  - **Description**: The PDF file containing the text for question generation.

### Response
```json
{
    "questions": [
        {
            "question": "What is the capital of France?",
            "option_A": "Paris",
            "option_B": "London",
            "option_C": "Berlin",
            "option_D": "Madrid",
            "correct_answer": "option_A"
        },
    ]
}
```

### Error Responses
- **400 Bad Request**
```json
{
    "error": "No PDF file selected"
}
```
- **500 Internal Server Error**
```json
{
    "error": "Failed to generate questions: <error message>"
}
```



## 3. Retrieve Questions

### Endpoint
```
GET /questions
```

### Description
Retrieve the generated multiple-choice questions stored in the session.

### Response
```json
{
    "questions": [
        {
            "question": "What is the capital of France?",
            "option_A": "Paris",
            "option_B": "London",
            "option_C": "Berlin",
            "option_D": "Madrid",
            "correct_answer": "option_A"
        },
    ]
}
```



## 4. Submit Answers

### Endpoint
```
POST /submit_answers
```

### Description
Submit answers for evaluation and receive results.

### Request
#### Headers
- `Content-Type`: `application/json`

#### Body
```json
{
    "answers": [
        {
            "question_id": "question_0",
            "selected_option": "option_A"
        },
    ]
}
```

### Response
```json
{
    "message": "Answers submitted successfully!",
    "score": 3,
    "total_questions": 5,
    "results": [
        {
            "question_id": "question_0",
            "question": "What is the capital of France?",
            "selected_option": "Paris",
            "correct_answer": "option_A",
            "options": {
                "option_A": "Paris",
                "option_B": "London",
                "option_C": "Berlin",
                "option_D": "Madrid"
            },
            "is_correct": true
        },
    ]
}
```



## 5. Retrieve Results

### Endpoint
```
GET /results
```

### Description
Retrieve the evaluation results stored in the session.

### Response
```json
{
    "score": 3,
    "total_questions": 5,
    "results": [
        {
            "question_id": "question_0",
            "question": "What is the capital of France?",
            "selected_option": "Paris",
            "correct_answer": "option_A",
            "options": {
                "option_A": "Paris",
                "option_B": "London",
                "option_C": "Berlin",
                "option_D": "Madrid"
            },
            "is_correct": true
        },
    ]
}
```



## 6. Error Handling

The API provides various error messages for different scenarios:
- If a PDF file is not uploaded, it returns a **400 Bad Request** with an appropriate error message.
- If there is an issue generating questions or saving to the database, it returns a **500 Internal Server Error** with details about the error.



## 7. Postman Instructions

To upload a PDF file using Postman, follow these steps:

1. **Open Postman**: Launch the Postman application.

2. **Create a New Request**:
   - Click on the **"+"** button to create a new tab.
   - Set the request type to `POST` from the dropdown on the left.

3. **Enter the URL**:
   - In the URL field, enter:
     ```
     https://quiz-setter.onrender.com/upload
     ```

4. **Select the Body Tab**:
   - Click on the **"Body"** tab below the URL field.

5. **Choose `form-data`**:
   - Select the **"form-data"** radio button.

6. **Add the PDF File**:
   - In the first column (Key), enter `pdf`.
   - In the second column (Value), click on the dropdown that says **"Text"** and change it to **"File"**.
   - Click on the **"Choose Files"** button that appears and select the PDF file from your computer.

7. **Send the Request**:
   - Click on the **"Send"** button to submit your request.

8. **View the Response**:
   - Check the response from the API in the lower part of the Postman window.
