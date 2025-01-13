Main Features
The application displays a trivia statement and the user has to guess if it is true by click on the green √ button, or false by clicking on the red x button.

If the user guesses correctly, the screen will flash green for 1 second, add a point to the user's score, and then advance to the next question.

Usage & Requirements
This project uses three libraries/packages:

TkInter
requests
html
And uses 3 classes:

Interface
QuizBrain
Question
And one data file:

data.py
Workflow
We first make a call to the Open Trivia Database API to retrieve the trivia questions by importing the data.py file into main.py:
from data import question_data
The data.py file call makes a requests.get() call to the API, converts the result to JSON, and then returns the data that we need to start the game:

def get_trivia_bank():
    response = requests.get(url="https://opentdb.com/api.php", params=params)
    response.raise_for_status()
    data = response.json()
    return data['results']


question_data = get_trivia_bank()
Next we sort through the question bank and pull only the data we need (the question text and the correct answer), storing it in a list:

question_bank = []
for question in question_data:
    question_text = question["question"]
    question_answer = question["correct_answer"]
    new_question = Question(question_text, question_answer)
    question_bank.append(new_question)
Lastly we send the filtered question data to the QuizBrain and start the Interface to begin the game:

quiz = QuizBrain(question_bank)
quiz_ui = Interface(quiz)
