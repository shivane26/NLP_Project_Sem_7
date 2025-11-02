# WordSense.io 🧠

WordSense.io is a web-based word-guessing game that challenges you to find a secret word. Unlike traditional guessing games, it uses a machine learning model to measure the **semantic similarity** between your guess and the target word, providing "Hot," "Warm," or "Cold" feedback based on how close you are in meaning.

![WordSense.io Gameplay Screenshot](https://i.imgur.com/example.png) 
## ✨ Features

* **Semantic Similarity:** Uses a real NLP model to understand the *meaning* of your guess, not just the letters.
* **Similarity Meter:** A dynamic progress bar that shows you exactly how "close" your guess is.
* **Helpful Hints:** Receive a hint every three guesses to help you narrow it down.
* **Stats Tracking:** Automatically saves your best score (fewest guesses) and current winning streak to your browser's local storage.
* **Difficulty Levels:** Choose from Easy, Medium, or Hard to change the pool of secret words.
* **Fully Client-Side:** The entire game, including the AI model, runs 100% in your browser. No server is needed, and it even works offline after the first load.

## 🛠️ Tech Stack

This project is built with a minimal stack, running entirely in the browser:

* **HTML:** The core structure of the game.
* **Tailwind CSS:** For all styling and UI components, loaded via a CDN.
* **JavaScript (ES6+):** For all game logic, state management, and DOM manipulation.
* **TensorFlow.js:** The core machine learning library for JavaScript.
* **Universal Sentence Encoder (USE):** A TensorFlow.js model used to convert words into semantic vectors (embeddings).
* **canvas-confetti:** For a fun celebration when you win!

## 🤖 How It Works

The core logic of the game relies on **text embeddings** and **cosine similarity**.

1.  **Model Load:** The **Universal Sentence Encoder** (USE) model is loaded into the browser via TensorFlow.js.
2.  **New Game:** A secret word (e.g., "king") is chosen from a predefined list. The game immediately uses the USE model to convert this word into a 512-dimension vector (an "embedding") that represents its meaning. This `secretWordVec` is stored.
3.  **Player Guess:** The player types a guess (e.g., "queen").
4.  **Embedding:** The game uses the same USE model to convert the guess "queen" into its own 512-dimension vector, `guessVec`.
5.  **Similarity Calculation:** The game calculates the **cosine similarity** between `secretWordVec` and `guessVec`. This is a mathematical formula that measures the angle between the two vectors, resulting in a score between -1 and 1 (though typically 0 to 1 in this context).
    * A score near `1.0` means the words are semantically identical or very close (e.g., "car" and "automobile").
    * A score near `0.0` means the words are semantically unrelated (e.g., "king" and "banana").
6.  **Feedback:** This similarity score is then translated into the "Hot"/"Cold" feedback and the width of the similarity bar, guiding the player's next guess.

## 🚀 How to Play

1.  **Open the Game:** The game starts with a "Play" button.
2.  **Model Load:** The first time you play, a loading screen will appear as the NLP model downloads (this is cached for future plays).
3.  **Guess:** Type a word into the input box and press "Guess" or "Enter".
4.  **Review Feedback:** Look at the guess history.
    * **Temperature:** "Hot" means you are very close in meaning. "Freezing" means you are very far.
    * **Similarity Meter:** The bar at the top shows a visual representation of your closeness.
5.  **Get Hints:** Every three guesses, a new hint will appear in the guess list.
6.  **Win:** Keep guessing until you find the secret word! A confetti explosion will celebrate your win.
7.  **New Game:** Click "New" to play again with a different word.

## 📁 How to Run Locally

This is a single-file project. No build steps or servers are required.

1.  Clone this repository or download the `index.html` file.
2.  Open the `index.html` file directly in any modern web browser (like Chrome, Firefox, or Edge).
3.  That's it! The game will load and play.
