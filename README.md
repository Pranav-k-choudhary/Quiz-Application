## Smart Quiz Application

A modern and interactive quiz application built using React, Context API, React Router, Hooks, and Bootstrap.

-> This project allows users to:
- Enter their name
- Attempt multiple quiz questions
- Track quiz progress with a progress bar
- Answer within a limited time
- View final score and percentage
- Store leaderboard data using Local Storage
- 
## Project Overview

The Smart Quiz Application is a frontend React project designed to test users with multiple-choice questions.

-> The application includes:
- Timer functionality
- Progress tracking
- Global state management using Context API + useReducer
- Routing using React Router
- Persistent leaderboard using browser Local Storage
- Lazy loading for better optimization

This project is beginner-friendly and demonstrates important React concepts used in real-world applications.

## Technologies Used
- React.js
- React Router DOM
- Context API
- useReducer Hook
- Custom Hooks
- Bootstrap 5
- Local Storage
- Vite

## Features
-> User Name Input:- Users must enter their name before starting the quiz.
-> Quiz Questions:- Questions are loaded from a JSON file.
-> Timer System:- Each question has a countdown timer of 15 seconds.
-> Progress Bar:- Displays quiz completion progress.
-> Score Tracking:- Tracks the number of correct answers.
-> Leaderboard:- Stores user scores permanently in Local Storage.
-> Responsive UI:- Built using Bootstrap for better responsiveness.
-> Lazy Loading:- Result page is lazy loaded using React.lazy().

## Complete Workflow

--> Application Starts

The application starts from:-

main.jsx
createRoot(document.getElementById('root')).render(
  <App />
)

Here:-
- React application is rendered
- Bootstrap CSS is imported
- App component is loaded


--> App Component:-

App.jsx

-> Responsibilities:-
- Wraps the entire app inside QuizProvider
- Handles routing using React Router
- Uses Suspense for lazy loading

-> Routes:-
- Route	Component
/	Home
/quiz	Quiz
/result	Result
/leaderboard	LeaderBoard


--> Global State Management

context/QuizContext.jsx

-> This file manages the complete application state using:
- createContext()
- useReducer()
- Reducer Actions
- Action	Purpose
- SET_NAME	Save username
- ANWSER	Update score and next question
- FINISH	Mark quiz completed
- RESET	Restart quiz


--> Home Page Workflow

pages/Home.jsx

-> Responsibilities
- Takes username input
- Starts the quiz
- Working Process
  
Step 1:
- User enters their name.

Step 2:
- Name is stored using:
- setName(e.target.value)
  
Step 3:
- When user clicks "Start Quiz":
- startQuiz()
  
Step 4:
-> The application:
  - Checks if input is empty
  - Dispatches SET_NAME action
  - Navigates to /quiz
  - dispatch({ type: "SET_NAME", payload: name })


--> Quiz Page Workflow

pages/Quiz.jsx

-> This is the main quiz engine.
-> Responsibilities
- Display questions
- Handle answers
- Handle timer
- Move to next question
- Finish quiz

--> Quiz Flow

Step 1: 
- Load Current Question
   const current = questions[index]
- The current question is selected using the question index.

Step 2: 
- Timer Starts
- Custom hook used:
    useTimer(15)
- Every question gets:
    15 seconds countdown
    Automatic reset after each question

Step 3: 
- Time Decreases Every Second

hooks/useTimer.js

setInterval(() => setTime(prev => prev - 1), 1000)

This reduces the timer every second.

Step 4: 
If Time Becomes 0
if(time === 0)
Then:
- Wrong answer is submitted automatically
- Next question loads

Step 5: 
- User Selects an Answer
- When user clicks an option:
- handleSelect(option)
- The app checks:
    option === current.answer
    If correct:
    Score increases
    Then:
       Question index increases
       Timer resets

Step 6: 
- Quiz Completion
If all questions are completed:
if(index >= questions.length)
Then:
dispatch({ type: "FINISH" })
And user is redirected to:

/result

-> Timer Component

components/Timer.jsx

- Purpose:
Display remaining time

Example:
⏳ Time Left: 10s

-> Progress Bar Component

components/ProgressBar.jsx

- Purpose:
Shows quiz progress percentage

Formula:
((current + 1) / total) * 100

Example:
60%


-> QuestionCard Component

components/QuestionCard.jsx

- Responsibilities:
    - Display question
    - Display options
    - Handle option click

Each option is rendered using:
options.map()


--> Result Page Workflow

pages/Result.jsx

-> Responsibilities
- Display score
- Calculate percentage
- Save leaderboard
- Reset quiz

-> Percentage Calculation
const percentage = Math.round(
  (state.score / state.questions.length) * 100
)

-> Saving Leaderboard
- Leaderboard data is stored in:
localStorage

Example:
localStorage.setItem(
  "leaderboard",
  JSON.stringify(updated)
)

- Stored data includes:
Name
Score
Percentage
Date


--> Leaderboard Workflow

pages/LeaderBoard.jsx

-> Responsibilities
- Fetch saved leaderboard data
- Display scores in table format
- Clear leaderboard

-> Data Fetching
JSON.parse(localStorage.getItem("leaderboard"))

-> Clear Leaderboard
localStorage.removeItem("leaderboard")

-> Questions Data

data/questions.json

Questions are stored in JSON format.


## Future Improvements
- Add category-wise quizzes
- Add dark mode
- Add authentication system
- Add backend database
- Add API-based questions
- Add sound effects
- Add difficulty levels
- Add negative marking
- Add quiz review section
- Add animations
