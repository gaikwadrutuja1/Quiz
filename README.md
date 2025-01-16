<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Java Quiz - Test Your Knowledge</title>
<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(to right, #00c6ff, #0072ff), url("images/java.png"); /* Combining gradient and background image */
    background-size: cover; /* Make sure the image covers the entire screen */
    background-position: center center; /* Center the image */
    background-attachment: fixed; /* Keeps the background fixed when scrolling */
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    text-align: center;
}

/* Styling for images around the box */
.java-img {
    position: absolute;
    max-width: 100px; /* Adjust size of images */
    opacity: 0.8; /* Slight transparency for better visibility */
}

.top-left {
    top: -30px;
    left: -30px;
}

.bottom-right {
    bottom: -30px;
    right: -30px;
}

.quiz-container {
    background-color: rgba(0, 0, 0, 0.7);
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
    width: 60%;
    text-align: left;
    position: relative; /* For absolute positioning of images */
}

/* Other Styles for the Quiz */
.question {
    font-size: 18px;
    margin: 10px 0;
}

.options {
    list-style: none;
    padding: 0;
}

.options li {
    margin: 10px 0;
    background-color: #fff;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.options li:hover {
    background-color: #f0f0f0;
}

.navigation {
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
}

#quiz-container {
    display: none;
}

/* Title Screen */
.title-screen {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
}

.title {
    font-size: 36px;
    margin-bottom: 20px;
    font-weight: bold;
    text-transform: uppercase;
}

button {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 20px;
}

button:hover {
    background-color: #45a049;
}

/* Quiz Section */
.quiz-container {
    background-color: rgba(0, 0, 0, 0.7);
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
    width: 60%;
    text-align: left;
}

.question {
    font-size: 18px;
    margin: 10px 0;
}

.options {
    list-style: none;
    padding: 0;
}

.options li {
    margin: 10px 0;
    background-color: #8f8cb7;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.options li:hover {
    background-color: #f0f0f0;
}

.navigation {
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
}

#result-screen {
    background-color: rgba(0, 0, 0, 0.7);
    padding: 40px;
    border-radius: 10px;
    width: 60%;
}

#score {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
}

#emoji {
    font-size: 48px;
}

#retry-btn {
    margin-top: 20px;
}

/* Hidden Elements */
#quiz-container, #result-screen {
    display: none;
}

</style></head>
<body>

  <!-- Title Screen -->
  <div id="title-screen" class="title-screen">
    <h1 class="title">Java Quiz - Test Your Knowledge</h1>
    <button id="start-btn" class="btn">Start Quiz</button>
  </div>

  <!-- Quiz Container -->
  <div id="quiz-container" class="quiz-container" style="display: none;">
    <div id="quiz"></div>
    <div class="navigation">
      <button id="previous-btn" class="btn" style="display: none;">Previous</button>
      <button id="next-btn" class="btn">Next</button>
    </div>
    <button id="submit" class="btn">Submit</button>
  </div>

  <!-- Result Screen -->
  <div id="result-screen" class="result-screen" style="display: none;">
    <h1>Your Score</h1>
    <div id="score"></div>
    <div id="emoji"></div>
    <button id="retry-btn" class="btn">Try Again</button>
  </div>

  <script>
  const quizData = [
    {
      question: "Which of the following is a primitive data type in Java?",
      options: ["String", "int", "ArrayList", "Object"],
      correctAnswer: 1
    },
    {
      question: "Which keyword is used to define a class in Java?",
      options: ["class", "define", "new", "type"],
      correctAnswer: 0
    },
    {
      question: "What is the size of the int data type in Java?",
      options: ["16 bit", "32 bit", "64 bit", "128 bit"],
      correctAnswer: 1
    },
    {
      question: "Which of the following is used to handle exceptions in Java?",
      options: ["try-catch", "if-else", "for-loop", "do-while"],
      correctAnswer: 0
    },
    {
      question: "Which method is used to start a thread in Java?",
      options: ["run()", "start()", "execute()", "initiate()"],
      correctAnswer: 1
    }
  ];
  
  let currentQuestionIndex = 0;
  let score = 0;
  
  function loadQuestion() {
    const quiz = document.getElementById('quiz');
    quiz.innerHTML = '';
  
    const questionData = quizData[currentQuestionIndex];
  
    const questionElement = document.createElement('div');
    questionElement.classList.add('question');
    questionElement.innerText = questionData.question;
  
    const optionsList = document.createElement('ul');
    optionsList.classList.add('options');
  
    questionData.options.forEach((option, index) => {
      const optionItem = document.createElement('li');
      const radioButton = document.createElement('input');
      radioButton.type = 'radio';
      radioButton.name = `question${currentQuestionIndex}`;
      radioButton.value = index;
  
      optionItem.appendChild(radioButton);
      optionItem.appendChild(document.createTextNode(option));
      optionsList.appendChild(optionItem);
    });
  
    quiz.appendChild(questionElement);
    quiz.appendChild(optionsList);
  }
  
  function showResult() {
    document.getElementById('quiz-container').style.display = 'none';
    document.getElementById('result-screen').style.display = 'block';
    const scoreElement = document.getElementById('score');
    const emojiElement = document.getElementById('emoji');
    
    scoreElement.innerText = `Your Score: ${score} / ${quizData.length}`;
  
    // Display emoji based on score
    if (score === quizData.length) {
      emojiElement.innerText = "🎉 Excellent! Perfect Score! 🎉";
    } else if (score >= quizData.length * 0.8) {
      emojiElement.innerText = "😁 Great Job! You're a Java Pro! 😁";
    } else if (score >= quizData.length * 0.5) {
      emojiElement.innerText = "🙂 Good Effort! Keep Practicing! 🙂";
    } else {
      emojiElement.innerText = "😞 Better Luck Next Time! 😞";
    }
  }
  
  document.getElementById('start-btn').addEventListener('click', () => {
    document.getElementById('title-screen').style.display = 'none';
    document.getElementById('quiz-container').style.display = 'block';
    loadQuestion();
  });
  
  document.getElementById('next-btn').addEventListener('click', () => {
    const selectedOption = document.querySelector(`input[name="question${currentQuestionIndex}"]:checked`);
    
    if (selectedOption) {
      const selectedAnswer = parseInt(selectedOption.value);
      const correctAnswer = quizData[currentQuestionIndex].correctAnswer;
  
      if (selectedAnswer === correctAnswer) {
        score++;
      }
    }
  
    currentQuestionIndex++;
    
    if (currentQuestionIndex < quizData.length) {
      loadQuestion();
      document.getElementById('previous-btn').style.display = 'inline-block'; // Show Previous Button
    } else {
      showResult();
    }
  });
  
  document.getElementById('previous-btn').addEventListener('click', () => {
    if (currentQuestionIndex > 0) {
      currentQuestionIndex--;
      loadQuestion();
    }
  });
  
  document.getElementById('retry-btn').addEventListener('click', () => {
    // Reset quiz
    currentQuestionIndex = 0;
    score = 0;
    document.getElementById('result-screen').style.display = 'none';
    document.getElementById('title-screen').style.display = 'flex';
  });
  
  </script>
</body>
</html>
