# React Quiz App - Project Overview

## 📌 What is This Project?

This is a **React-based Quiz Application** that tests users' knowledge about React. It's an interactive web app where users can take a quiz with multiple-choice questions, receive instant feedback, and track their scores.

---

## 🎯 Main Features

1. **Welcome Screen** - Start the quiz
2. **Question Display** - Shows one question at a time with 4 options
3. **Real-time Scoring** - Points are awarded for correct answers
4. **Timer** - 30 seconds per question countdown
5. **Progress Tracking** - See how many questions you've answered and current score
6. **Finish Screen** - Shows final score, percentage, emoji feedback, and high score
7. **Restart Option** - Retake the quiz and try to beat your high score

---

## 🏗️ Project Structure

```
├── src/
│   ├── App.jsx              (Main component - handles the entire quiz logic)
│   ├── Components/          (All smaller UI components)
│   │   ├── Header.jsx       (App title/header)
│   │   ├── StartScreen.jsx  (Welcome screen)
│   │   ├── Question.jsx     (Question display)
│   │   ├── Options.jsx      (Multiple choice buttons)
│   │   ├── NextButton.jsx   (Next question button)
│   │   ├── Progress.jsx     (Score & question progress)
│   │   ├── FinishScreen.jsx (Results screen)
│   │   ├── Timer.jsx        (Countdown timer)
│   │   ├── Loader.jsx       (Loading spinner)
│   │   ├── Error.jsx        (Error message)
│   │   └── Other components
│   ├── App.css
│   └── index.css
└── data/
    └── questions.json       (Quiz questions database)
```

---

## 📊 How Data Flows (The Big Picture)

```
┌─────────────────────┐
│  questions.json     │  (Data source)
│  (Quiz questions)   │
└──────────┬──────────┘
           │
           ├→ fetch() in App.jsx
           │
           ↓
┌─────────────────────┐
│  App State (Redux  │  (Reducer manages all app data)
│  Pattern with      │   - status (loading/ready/active/finished)
│  useReducer)       │   - questions list
│                    │   - current index
│                    │   - user answer
│                    │   - points
└────────┬───────────┘
         │
         ├→ Dispatches Actions
         │   (type: "start", "newAnswer", etc.)
         │
         ↓
┌─────────────────────────────────────┐
│    Conditional Rendering            │
│  Shows different screens based       │
│  on current status:                  │
│  - Loading → Loader                 │
│  - Ready → StartScreen              │
│  - Active → Question + Timer        │
│  - Finished → FinishScreen          │
└─────────────────────────────────────┘
```

---

## 🔄 State Management (The Core Logic)

The app uses **useReducer hook** which is like a state management system. Think of it as a machine:

- **Input**: Current state + Action
- **Output**: New state

### Key State Properties:

| Property           | Purpose                                                            |
| ------------------ | ------------------------------------------------------------------ |
| `questions`        | Array of all quiz questions                                        |
| `status`           | Current screen ("loading", "error", "ready", "active", "finished") |
| `index`            | Which question are we on (0 to numQuestions-1)                     |
| `answer`           | User's selected answer for current question (null = no answer yet) |
| `points`           | Total score accumulated so far                                     |
| `highscore`        | Best score from previous attempts                                  |
| `secondsRemaining` | Time left for the quiz                                             |

---

## 🎮 User Journey (Step by Step)

### 1️⃣ **App Loads**

```
- Fetch questions from http://localhost:8000/questions
- Status changes from "loading" → "ready"
- StartScreen appears with "Let's Start" button
```

### 2️⃣ **User Clicks "Let's Start"**

```
- Action: { type: "start" }
- Timer starts (30 seconds × number of questions)
- Status changes from "ready" → "active"
- First question displays with 4 option buttons
```

### 3️⃣ **User Clicks an Option**

```
- Action: { type: "newAnswer", payload: selectedIndex }
- App checks if answer is correct
- If correct: points += question.points
- Buttons become disabled (can't change answer)
- Correct answer highlights in GREEN
- Wrong answers highlight in RED
```

### 4️⃣ **User Clicks "Next →"**

```
- Action: { type: "nextQuestion" }
- Move to next question (index++)
- Reset answer to null
- Buttons become enabled again
```

### 5️⃣ **Timer Reaches Zero OR All Questions Answered**

```
- Action: { type: "finish" }
- Status changes from "active" → "finished"
- FinishScreen shows:
  - Final score and percentage
  - Emoji reaction based on performance
  - High score comparison
```

### 6️⃣ **User Clicks "Restart"**

```
- Action: { type: "restart" }
- Reset to beginning (index = 0, answer = null, points = 0)
- Keep highscore if they did better
- Status goes back to "ready"
```

---

## 📝 Data Example (questions.json)

Each question has:

```json
{
  "question": "Which is the most popular JavaScript framework?",
  "options": ["Angular", "React", "Svelte", "Vue"],
  "correctOption": 1, // Index of correct answer (React = index 1)
  "points": 10 // Points for getting it right
}
```

---

## ⚙️ Key Components Explained

### **App.jsx** (The Brain)

- Contains all the quiz logic
- Uses useReducer to manage state
- Fetches questions from server
- Conditionally renders different screens

### **StartScreen.jsx**

- Simple welcome message
- "Let's Start" button dispatches start action

### **Question.jsx + Options.jsx**

- Question.jsx displays the question text
- Options.jsx shows 4 clickable answer buttons
- Changes styling based on:
  - Whether user has answered
  - Which answer is correct

### **Progress.jsx**

- Shows: "Question X of Y"
- Shows current score and max possible points

### **Timer.jsx**

- Countdown timer (using useEffect and setInterval)
- Each second dispatches { type: "tick" }
- When reaches 0, auto-finishes the quiz

### **FinishScreen.jsx**

- Shows score, percentage, and emoji
- Displays high score
- Restart button

---

## 🚀 How to Run

1. **Start the JSON server** (in terminal):

```bash
npm run server
```

2. **Start the React app** (in another terminal):

```bash
npm run dev
```

3. Open http://localhost:5173 in your browser

---

## 🔑 Key React Concepts Used

1. **useState/useReducer** - State management
2. **useEffect** - Side effects (fetching data, timer)
3. **Component composition** - Breaking UI into smaller reusable pieces
4. **Props** - Passing data and functions to child components
5. **Conditional rendering** - Showing/hiding content based on state
6. **Event handling** - Click handlers and form interactions
7. **Array methods** - map(), reduce() for processing questions and calculating scores

---

## 💡 Learning Tips

- **Understand the reducer first**: It's the heart of this app
- **Trace the data flow**: Follow how actions → state changes → re-renders
- **Component hierarchy**: See how components receive data via props
- **why useReducer?**: It's better than multiple useState for complex state logic

Good luck learning! 🎉
