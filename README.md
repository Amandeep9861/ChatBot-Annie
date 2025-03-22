#INDEX.HTML
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Annie - Customer Support Bot</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <div class="chat-container">
        <div class="chat-header">
            <img src="https://i.ibb.co/0MZ8kt4/bot-avatar.png" alt="Annie Avatar" class="bot-avatar" />
            Annie - Customer Support Bot 💬
        </div>
        <div class="chat-box" id="chat-box"></div>
        <div class="typing-indicator" id="typing-indicator">Annie is typing...</div>
        <div class="chat-input">
            <input type="text" id="user-input" placeholder="Type your message..." />
            <button id="send-btn">Send</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>

</html>


</html>
   #STYLE.CSS
   body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #74ebd5, #9face6);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.chat-container {
    width: 400px;
    height: 600px;
    background: #ffffff;
    border-radius: 15px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
    display: flex;
    flex-direction: column;
    overflow: hidden;
    border: 2px solid #6a11cb;
    position: relative;
}

.chat-header {
    background: linear-gradient(90deg, #6a11cb, #2575fc);
    color: #fff;
    padding: 20px;
    text-align: center;
    font-weight: bold;
    font-size: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.bot-avatar {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background: #fff;
}

.chat-box {
    flex: 1;
    padding: 10px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
    background: #f1f6fb;
}

.chat-message {
    padding: 12px 16px;
    border-radius: 10px;
    max-width: 75%;
    line-height: 1.4;
    word-wrap: break-word;
    font-size: 15px;
}

.user-message {
    background: #c1e1c1;
    align-self: flex-end;
}

.bot-message {
    background: #fef3c7;
    align-self: flex-start;
    border: 1px solid #fcd34d;
}

.bot-options {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 5px;
}

.bot-options button {
    background: #6a11cb;
    color: #fff;
    border: none;
    padding: 8px 12px;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.bot-options button:hover {
    background: #2575fc;
}

.chat-input {
    display: flex;
    border-top: 1px solid #ddd;
}

.chat-input input {
    flex: 1;
    padding: 14px;
    border: none;
    outline: none;
}

.chat-input button {
    background: #6a11cb;
    color: #fff;
    border: none;
    padding: 0 25px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.chat-input button:hover {
    background: #2575fc;
}

.typing-indicator {
    display: none;
    text-align: left;
    color: #555;
    font-size: 13px;
    padding: 5px 10px;
}
#SCRIPT.JS
document.getElementById('send-btn').addEventListener('click', handleUserInput);
document.getElementById('user-input').addEventListener('keypress', function (e) {
    if (e.key === 'Enter') handleUserInput();
});

function handleUserInput() {
    const userInput = document.getElementById('user-input').value;
    if (userInput.trim() !== '') {
        addMessage(userInput, 'user');
        document.getElementById('user-input').value = '';
        showTyping();
        setTimeout(() => {
            handleBotResponse(userInput);
            hideTyping();
        }, 1000);
    }
}

function addMessage(message, sender) {
    const chatBox = document.getElementById('chat-box');
    const messageDiv = document.createElement('div');
    messageDiv.className = `chat-message ${sender}-message`;
    messageDiv.innerText = message;
    chatBox.appendChild(messageDiv);
    chatBox.scrollTop = chatBox.scrollHeight;
}

function handleBotResponse(userInput) {
    const lowerCaseInput = userInput.toLowerCase();

    if (lowerCaseInput.includes('hello') || lowerCaseInput.includes('hi')) {
        addMessage("Hello! I'm Annie, your support assistant. 😊 How can I help you today?", 'bot');
    } else if (lowerCaseInput.includes('complaint') || lowerCaseInput.includes('issue')) {
        showComplaintOptions();
    } else {
        addMessage("I'm here to help! If you want to file a complaint, just type 'complaint'.", 'bot');
    }
}

function showComplaintOptions() {
    const chatBox = document.getElementById('chat-box');
    const messageDiv = document.createElement('div');
    messageDiv.className = 'chat-message bot-message';
    messageDiv.innerText = "Please select the type of complaint:";

    const optionsDiv = document.createElement('div');
    optionsDiv.className = 'bot-options';

    const complaints = ['Product Issue', 'Late Delivery', 'Wrong Item', 'Other'];

    complaints.forEach(complaint => {
        const button = document.createElement('button');
        button.innerText = complaint;
        button.addEventListener('click', () => {
            addMessage(complaint, 'user');
            showTyping();
            setTimeout(() => {
                addMessage(`Thank you! I've logged your complaint about "${complaint}". Our team will reach out shortly! 🙌`, 'bot');
                hideTyping();
            }, 1000);
        });
        optionsDiv.appendChild(button);
    });

    messageDiv.appendChild(optionsDiv);
    chatBox.appendChild(messageDiv);
    chatBox.scrollTop = chatBox.scrollHeight;
}

function showTyping() {
    document.getElementById('typing-indicator').style.display = 'block';
}

function hideTyping() {
    document.getElementById('typing-indicator').style.display = 'none';
}

window.onload = function () {
    showTyping();
    setTimeout(() => {
        addMessage("👋 Hi there! I'm Annie. Type 'hello' or 'complaint' to get started.", 'bot');
        hideTyping();
    }, 1000);
};

<img width="480" alt="image" src="https://github.com/user-attachments/assets/1239a436-7789-4c99-a683-086041c457ed" />
