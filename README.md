<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Жасанды Интеллект Чат</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            text-align: center;
            padding: 50px;
        }
        .chat-box {
            width: 80%;
            max-width: 600px;
            margin: auto;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 10px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            height: 300px;
            overflow-y: scroll;
        }
        .input-box {
            width: 80%;
            padding: 10px;
            margin-top: 10px;
        }
        .send-btn {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .send-btn:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <h1>Жасанды Интеллектпен сөйлесу</h1>
    <div class="chat-box" id="chat-box"></div>
    <input type="text" id="user-input" class="input-box" placeholder="Сұрақ қойыңыз...">
    <button class="send-btn" onclick="sendMessage()">Жіберу</button>

    <script>
        async function sendMessage() {
            const userInput = document.getElementById('user-input').value;
            const chatBox = document.getElementById('chat-box');
            
            if (userInput) {
                chatBox.innerHTML += `<div><strong>Сіз:</strong> ${userInput}</div>`;
                
                // OpenAI API арқылы жауап алу
                const response = await getAIResponse(userInput);
                
                chatBox.innerHTML += `<div><strong>Жасанды Интеллект:</strong> ${response}</div>`;
                document.getElementById('user-input').value = '';
                chatBox.scrollTop = chatBox.scrollHeight;
            }
        }

        async function getAIResponse(userInput) {
            const apiKey = 'sk-z9vAC3kfHmY8rgg0mxI4UdP9nF81x';  // OpenAI API кілтін осында қойыңыз
            const response = await fetch('https://api.openai.com/v1/completions', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${apiKey}`
                },
                body: JSON.stringify({
                    model: "text-davinci-003",  // Немесе жаңа модель
                    prompt: userInput,
                    max_tokens: 150
                })
            });
            const data = await response.json();
            return data.choices[0].text.trim();
        }
    </script>
</body>
</html>
