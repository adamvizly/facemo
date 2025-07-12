# AI Emotion & Speech Log

![AI Emotion Log Screenshot](https://placehold.co/800x450/3b82f6/ffffff?text=App+Screenshot+Here)

A real-time, browser-based web application that uses your webcam and microphone to analyze facial expressions and transcribe speech. It creates a synchronized log of what you say and the dominant emotion you're expressing at that moment.

**[➡️ View Live Demo](https://your-github-username.github.io/your-repo-name/)** *(Replace with your GitHub Pages link after deployment)*

---

## ✨ Features

* **Real-Time Video Analysis:** Captures your webcam feed directly in the browser.
* **Facial Emotion Recognition:** Utilizes machine learning models to detect 7 different emotions (happy, sad, angry, neutral, surprised, disgusted, fearful) from the video stream.
* **Live Speech-to-Text:** Uses the browser's built-in Web Speech API to transcribe your speech as you talk.
* **Synchronized Logging:** Intelligently pairs the transcribed text with the emotion detected at the moment of speech.
* **Zero Backend:** The entire application runs client-side. No data is sent to a server, ensuring user privacy.
* **Responsive Design:** A clean and modern UI that works on both desktop and mobile devices.

---

## 🛠️ Technologies Used

This project is built entirely with client-side web technologies:

* **HTML5:** For the structure of the application.
* **Tailwind CSS:** For modern, responsive styling.
* **JavaScript (ES6+):** For all the application logic.
* **[Face-api.js](https://github.com/justadudewhohacks/face-api.js/):** A powerful JavaScript module built on top of TensorFlow.js for face detection and facial expression recognition in the browser.
* **WebRTC (`getUserMedia`):** A browser API to securely access the user's camera and microphone.
* **Web Speech API (`SpeechRecognition`):** A browser API for performing speech-to-text.

---

## 🚀 How to Run Locally

Since this is a purely front-end application, running it locally is very simple.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-github-username/your-repo-name.git](https://github.com/your-github-username/your-repo-name.git)
    ```

2.  **Navigate to the project directory:**
    ```bash
    cd your-repo-name
    ```

3.  **Open the `index.html` file:**
    You can't just open the `index.html` file directly from the file system because of browser security policies (CORS) related to loading the AI models. You need to serve it from a local server. The easiest way is to use the `Live Server` extension in VS Code.
    * Right-click the `index.html` file in VS Code.
    * Select "Open with Live Server".

    This will open the application in your default browser, and it will ask for camera and microphone permissions.

---

## ⚙️ How It Works

The application's logic is based on running two processes in parallel and synchronizing their outputs.

1.  **Initialization:** On page load, the app first requests access to the user's webcam and microphone. Simultaneously, it loads the pre-trained `face-api.js` models required for face and emotion detection.
2.  **Emotion Detection Loop:** Once the "Start Session" button is clicked, a `setInterval` loop begins. Every 700ms, it captures the current frame from the `<video>` element and passes it to `face-api.js`. The API returns the dominant emotion, which is stored in a global `currentEmotion` variable.
3.  **Speech Recognition:** The Web Speech API listens continuously for the user to speak. It processes audio and provides interim results as the user talks.
4.  **Synchronization:** When the Speech API determines that a user has finished a phrase (an `isFinal` result), it fires an event containing the final transcribed text. At this exact moment, the application grabs the `currentEmotion` variable and pairs it with the transcribed text.
5.  **Logging:** The final text and its corresponding emotion are then formatted and appended to the analysis log on the right-hand side of the screen.

---

## 📄 License

This project is open source and available under the [MIT License].