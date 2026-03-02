# ⚛️ React Quiz App

An interactive quiz application built with React that tests your knowledge of React concepts. Answer multiple-choice questions, race against the clock, and try to beat your high score!

---

## 🎯 Features

- **Welcome Screen** – Clean start screen to kick off the quiz
- **One Question at a Time** – Focused question display with 4 answer options
- **Real-time Scoring** – Points awarded instantly for correct answers
- **Countdown Timer** – 30 seconds per question to keep you on your toes
- **Progress Tracking** – See your current question number and score at a glance
- **Results Screen** – Final score, percentage, emoji feedback, and high score tracking
- **Restart Option** – Retake the quiz and try to beat your personal best

---

## 🏗️ Project Structure

```
├── src/
│   ├── App.jsx              # Main component – handles all quiz logic
│   ├── Components/
│   │   ├── Header.jsx       # App title/header
│   │   ├── StartScreen.jsx  # Welcome screen
│   │   ├── Question.jsx     # Question display
│   │   ├── Options.jsx      # Multiple choice buttons
│   │   ├── NextButton.jsx   # Next question button
│   │   ├── Progress.jsx     # Score & question progress
│   │   ├── FinishScreen.jsx # Results screen
│   │   ├── Timer.jsx        # Countdown timer
│   │   ├── Loader.jsx       # Loading spinner
│   │   └── Error.jsx        # Error message
│   ├── App.css
│   └── index.css
└── data/
    └── questions.json       # Quiz questions database
```

---

## 🚀 Getting Started

**1. Start the JSON server** (in one terminal):
```bash
npm run server
```

**2. Start the React app** (in another terminal):
```bash
npm run dev
```

**3.** Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 📊 How It Works

The app uses a **`useReducer`** hook for state management, following a Redux-like pattern:

```
questions.json  →  fetch() in App.jsx  →  useReducer state  →  Conditional rendering
```

### App States

| Status | Screen Shown |
|--------|-------------|
| `loading` | Loader spinner |
| `error` | Error message |
| `ready` | Start Screen |
| `active` | Question + Timer |
| `finished` | Results Screen |

### State Properties

| Property | Purpose |
|----------|---------|
| `questions` | Array of all quiz questions |
| `status` | Current screen/phase of the app |
| `index` | Current question index |
| `answer` | User's selected answer (`null` = unanswered) |
| `points` | Accumulated score |
| `highscore` | Best score from all attempts |
| `secondsRemaining` | Time left on the countdown |

---

## 🎮 User Journey

1. **App loads** → Questions are fetched → Start Screen appears
2. **Click "Let's Start"** → Timer begins, first question displays
3. **Select an answer** → Correct answer highlights green, wrong ones red; points awarded if correct
4. **Click "Next →"** → Advance to the next question
5. **Quiz ends** (all questions answered or timer runs out) → Results Screen shows score, percentage, and emoji
6. **Click "Restart"** → Reset the quiz, high score is preserved

---

## 📝 Question Format

Each question in `questions.json` follows this structure:

```json
{
  "question": "Which is the most popular JavaScript framework?",
  "options": ["Angular", "React", "Svelte", "Vue"],
  "correctOption": 1,
  "points": 10
}
```

---

## 🔑 Key React Concepts Used

- `useReducer` & `useState` – State management
- `useEffect` – Data fetching and timer logic
- **Component Composition** – Modular, reusable UI components
- **Props** – Passing data and callbacks to child components
- **Conditional Rendering** – Displaying the right screen based on app state
- **Event Handling** – Click handlers for answers and navigation
- **Array Methods** – `map()`, `reduce()` for rendering and score calculation

---

## 🛠️ Tech Stack

- [React](https://react.dev/)
- [Vite](https://vitejs.dev/)
- [JSON Server](https://github.com/typicode/json-server) – Mock REST API for questions

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
