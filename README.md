Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ChatGPT Clone</title>
    <link rel="stylesheet" href="j.css">
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">
            <div class="header-left">
                <button class="menu-btn">☰</button>
                <h1>ChatGPT</h1>
            </div>
            <button class="login-btn">Log in</button>
        </div>

        <div class="chat-welcome">
            <h2>What can I help with?</h2>
            <div class="quick-actions">
                <button class="action-btn">📄 Summarize text</button>
                <button class="action-btn">💡 Make a plan</button>
                <button class="action-btn">🧠 Brainstorm</button>
                <button class="action-btn">💻 Code</button>
                <button class="action-btn">➕ More</button>
            </div>
        </div>

        <div class="chat-box" id="chat-box"></div>

        <div class="input-area">
            <button class="attach-btn">➕ Attach</button>
            <button class="search-btn">🌍 Search</button>
            <button class="reason-btn">💡 Reason</button>
            <input type="text" id="user-input" placeholder="Ask anything..." onkeypress="handleEnter(event)">
            <button onclick="sendMessage()">➤</button>
        </div>

        <div class="footer">
            By messaging ChatGPT, you agree to our <a href="#">Terms</a> and <a href="#">Privacy Policy</a>.
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>


JS
function sendMessage() {
    let userInput = document.getElementById("user-input");
    let chatBox = document.getElementById("chat-box");

    let message = userInput.value.trim();
    if (message === "") return;

    appendMessage("user-message", message);

    let botTyping = document.createElement("div");
    botTyping.classList.add("bot-message", "typing");
    botTyping.innerText = "Typing...";
    chatBox.appendChild(botTyping);
    chatBox.scrollTop = chatBox.scrollHeight;

    setTimeout(() => {
        chatBox.removeChild(botTyping);
        botReply(message);
    }, 1000);

    userInput.value = "";
    chatBox.scrollTop = chatBox.scrollHeight;
}

function appendMessage(className, text) {
    let chatBox = document.getElementById("chat-box");
    let messageDiv = document.createElement("div");
    messageDiv.classList.add(className);
    messageDiv.innerText = text;
    chatBox.appendChild(messageDiv);
    chatBox.scrollTop = chatBox.scrollHeight;
}

function botReply(userMessage) {
    let responses = {
        "hello": "Hello! How can I assist you today?",
        "how are you": "I'm just an AI, but I'm always here to help!",
        "who are you": "I'm a ChatGPT clone built using HTML, CSS, and JavaScript.",
        "default": "I'm not sure about that. Try asking something else!"
    };

    let lowerCaseMessage = userMessage.toLowerCase();
    let reply = responses[lowerCaseMessage] || responses["default"];

    appendMessage("bot-message", reply);
}

function handleEnter(event) {
    if (event.key === "Enter") {
        sendMessage();
    }
}

CSS
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #202123;
    color: white;
}

.chat-container {
    width: 100%;
    max-width: 500px;
    height: 700px;
    background: #343541;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.chat-header {
    background: #202123;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
}

.header-left {
    display: flex;
    align-items: center;
}

.menu-btn {
    background: none;
    border: none;
    font-size: 20px;
    color: white;
    margin-right: 10px;
}

.login-btn {
    background: white;
    color: black;
    padding: 5px 15px;
    border-radius: 15px;
    border: none;
    font-size: 14px;
    cursor: pointer;
}

.chat-welcome {
    text-align: center;
    padding: 20px;
}

.quick-actions {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    margin-top: 15px;
}

.action-btn {
    background: #2d2e36;
    border: none;
    padding: 10px 15px;
    border-radius: 20px;
    color: white;
    cursor: pointer;
    font-size: 14px;
}

.chat-box {
    flex: 1;
    padding: 15px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
}

.input-area {
    display: flex;
    align-items: center;
    padding: 10px;
    background: #40414f;
    gap: 5px;
}

.attach-btn, .search-btn, .reason-btn {
    background: #2d2e36;
    border: none;
    padding: 8px;
    border-radius: 10px;
    color: white;
    font-size: 14px;
    cursor: pointer;
}

input {
    flex: 1;
    padding: 12px;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    background: #343541;
    color: white;
}

button {
    border: none;
    background: #0fa37f;
    color: white;
    padding: 10px 15px;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
}

button:hover {
    background: #08926b;
}

.footer {
    text-align: center;
    padding: 10px;
    font-size: 12px;
    background: #202123;
}

.footer a {
    color: #0fa37f;
    text-decoration: none;
}
