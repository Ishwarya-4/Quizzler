# 🧠 Quizzler

A True/False quiz app with a graphical interface built using Python, `tkinter`, and the [Open Trivia Database (OpenTDB)](https://opentdb.com/) API. Questions are fetched live from the internet every time you play, so no two rounds are the same.

---

## 🖥️ App Preview

The quiz window displays one question at a time on a card. Click ✅ for **True** or ❌ for **False**. The card flashes **green** for a correct answer and **red** for an incorrect one before automatically advancing to the next question. Your live score is shown in the top-right corner. When all 10 questions are done, the buttons disable and the quiz ends.

---

## 🗂️ Project Structure

```
Quizzler/
├── main.py              # Entry point — builds the question bank and launches the UI
├── data.py              # Fetches 10 True/False questions from the OpenTDB API
├── question_model.py    # Question class (data model)
├── quiz_brain.py        # QuizBrain class (game logic & answer checking)
├── ui.py                # QuizInterface class (tkinter GUI)
└── images/
    ├── true.png         # ✅ True button image
    └── false.png        # ❌ False button image
```

---

## 🧱 Classes Overview

### `Question` *(question_model.py)*
A simple data model holding a single question's text and its correct answer (`"True"` or `"False"`).

### `QuizBrain` *(quiz_brain.py)*
The game engine. Tracks the current question number and score, advances through the question list, and validates user answers. Uses Python's built-in `html` module to decode HTML entities in question text (e.g. `&amp;` → `&`).

| Method | Description |
|---|---|
| `still_has_questions()` | Returns `True` while questions remain |
| `next_question()` | Advances to the next question and returns its formatted text |
| `check_answer(user_answer)` | Compares user input to the correct answer, increments score if correct |

### `QuizInterface` *(ui.py)*
The full `tkinter` GUI. Displays the score label, question canvas, and True/False image buttons. After each answer, the canvas background flashes green or red for 1 second before loading the next question. Disables buttons when the quiz is complete.

### `data.py`
Fetches 10 boolean (True/False) questions from the OpenTDB API on startup using the `requests` library. The app always plays with fresh, unique questions.

---

## 🚀 Getting Started

**Prerequisites:** Python 3.x

Install the one required third-party library:

```bash
pip install requests
```

Then clone and run:

```bash
git clone https://github.com/Ishwarya-4/Quizzler.git
cd Quizzler
python main.py
```

> An active internet connection is required to fetch questions from the OpenTDB API.

---

## ✨ Features

- **Live questions** — 10 fresh True/False trivia questions pulled from the web each session
- **Instant visual feedback** — canvas turns green ✅ or red ❌ after every answer
- **Live score tracking** — score updates in real time in the top-right corner
- **Auto-advance** — moves to the next question after a 1-second feedback pause
- **Clean GUI** — built entirely with `tkinter`, no external UI frameworks needed
- **HTML entity handling** — question text is decoded correctly (e.g. apostrophes, symbols)

---

## 🔌 API Reference

Questions are sourced from the [Open Trivia Database](https://opentdb.com/):

```
GET https://opentdb.com/api.php?amount=10&type=boolean
```

| Parameter | Value | Description |
|---|---|---|
| `amount` | 10 | Number of questions per session |
| `type` | boolean | Returns True/False questions only |

---

## 🧠 OOP & Python Concepts Demonstrated

- **Classes & Objects** — each component (question, logic, UI) has its own class
- **Encapsulation** — quiz state and UI state are managed independently within their classes
- **Type hints** — `QuizInterface.__init__` uses `quiz_brain: QuizBrain` as a type annotation
- **API integration** — live HTTP GET request using the `requests` library
- **GUI programming** — `tkinter` canvas, labels, buttons, image handling, and event callbacks
- **`html.unescape()`** — handles encoded characters in API response text
