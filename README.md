# YAPAYZEKA.COM
basit ve deneme amaçlı bir yapay zeka 
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Benim Akıllı Yapay Zekam</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0f172a;
            color: #f8fafc;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        .chat-container {
            width: 100%;
            max-width: 600px;
            height: 80vh;
            background: #1e293b;
            border-radius: 16px;
            display: flex;
            flex-direction: column;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            overflow: hidden;
            border: 1px solid #334155;
        }
        .chat-header {
            background: #0284c7;
            padding: 16px;
            font-size: 18px;
            font-weight: bold;
            text-align: center;
        }
        .chat-messages {
            flex: 1;
            padding: 16px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .message {
            padding: 12px 16px;
            border-radius: 12px;
            max-width: 80%;
            line-height: 1.5;
            word-wrap: break-word;
        }
        .user-message {
            background: #3b82f6;
            color: white;
            align-self: flex-end;
            border-bottom-right-radius: 2px;
        }
        .ai-message {
            background: #334155;
            color: #f1f5f9;
            align-self: flex-start;
            border-bottom-left-radius: 2px;
        }
        .chat-input-area {
            display: flex;
            padding: 12px;
            background: #0f172a;
            border-top: 1px solid #334155;
        }
        input {
            flex: 1;
            padding: 12px;
            border: 1px solid #475569;
            border-radius: 8px;
            background: #1e293b;
            color: white;
            font-size: 16px;
            outline: none;
        }
        input:focus {
            border-color: #38bdf8;
        }
        button {
            background: #0284c7;
            color: white;
            border: none;
            padding: 0 20px;
            margin-left: 8px;
            border-radius: 8px;
            font-size: 16px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
        }
        button:hover {
            background: #0369a1;
        }
    </style>
</head>
<body>

    <div class="chat-container">
        <div class="chat-header">🤖 Benim Özel Yapay Zeka Asistanım</div>
        <div class="chat-messages" id="chatMessages">
            <div class="message ai-message">Selam kanka! Ben senin yapay zeka asistanınım. Bana dilediğin soruyu sorabilirsin!</div>
        </div>
        <div class="chat-input-area">
            <input type="text" id="userInput" placeholder="Bir şeyler yaz..." onkeypress="handleKeyPress(event)">
            <button onclick="sendMessage()">Gönder</button>
        </div>
    </div>

    <script>
        const messagesContainer = document.getElementById('chatMessages');
        const userInput = document.getElementById('userInput');

        function appendMessage(text, sender) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('message');
            messageDiv.classList.add(sender === 'user' ? 'user-message' : 'ai-message');
            messageDiv.textContent = text;
            messagesContainer.appendChild(messageDiv);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }

        async function sendMessage() {
            const text = userInput.value.trim();
            if (!text) return;

            appendMessage(text, 'user');
            userInput.value = '';

            // Geçici "düşünüyor..." mesajı ekle
            const loadingId = 'loading-' + Date.now();
            const loadingDiv = document.createElement('div');
            loadingDiv.classList.add('message', 'ai-message');
            loadingDiv.id = loadingId;
            loadingDiv.textContent = "Düşünüyorum...";
            messagesContainer.appendChild(loadingDiv);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;

            try {
                // Burada gerçek bir yapay zeka servisine (örn: Gemini API veya yerel simülasyon) bağlanabilirsin.
                // Şimdilik tarayıcının kendi gücüyle simüle eden veya akıllı yanıt üreten mantığı kuruyoruz:
                setTimeout(() => {
                    document.getElementById(loadingId).remove();
                    
                    let aiResponse = "";
                    const lowerText = text.toLowerCase();

                    if (lowerText.includes('merhaba') || lowerText.includes('selam')) {
                        aiResponse = "Aleykümselam kanka! Projemiz nasıl gidiyor?";
                    } else if (lowerText.includes('nasılsın')) {
                        aiResponse = "Kodlar harika akıyor, sen nasılsın?";
                    } else if (lowerText.includes('yapay zeka')) {
                        aiResponse = "Evet! Şu an senin yazdığın arayüz üzerinden seninle konuşuyorum. Dünyayı ele geçirmemize az kaldı 😎";
                    } else {
                        aiResponse = `Harika bir soru: "${text}". Bunu tüm derinliğimle inceledim ve şunu söyleyebilirim: Sen bu işi çözüyorsun kanka! Gerçek bir API bağladığında burası doğrudan Google/OpenAI sunucularına bağlanacak.`;
                    }

                    appendMessage(aiResponse, 'ai');
                }, 1000);

            } catch (error) {
                document.getElementById(loadingId).remove();
                appendMessage("Bir hata oluştu kanka.", 'ai');
            }
        }

        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                sendMessage();
            }
        }
    </script>

</body>
</html>
