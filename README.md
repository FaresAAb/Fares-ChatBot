# 🚀 Fares's AI ChatBot

A simple AI-powered chatbot using **Langchain Ollama** with a Flask API and a command-line chatbot interface.

## 📌 Features
- **Flask API** to interact via HTTP requests.
- **Command-line chatbot** for local use.
- **Context handling** (keeps track of conversation history).
- **Logging system** (stores chat history in a file).

---

## 🛠 Installation & Setup
### **1️⃣ Install Python**
Ensure you have **Python 3.10+** installed. Check your version:
```sh
python --version
```
If not installed, download Python from [python.org](https://www.python.org/downloads/).

### **2️⃣ Clone the Repository**
```sh
git clone https://github.com/YOUR_GITHUB_USERNAME/FaresChatBot.git
cd FaresChatBot
```

### **3️⃣ Set Up a Virtual Environment**
```sh
python -m venv env
```
Activate the virtual environment:
- **Windows:**
  ```sh
  ./env/Scripts/activate
  ```
- **Mac/Linux:**
  ```sh
  source env/bin/activate
  ```

### **4️⃣ Install Dependencies**
```sh
pip install -r requirements.txt
```
Create a `requirements.txt` file with:
```
flask
langchain_ollama
```

---

## 🚀 Running the ChatBot

### **🔹 Run Flask API (app.py)**
```sh
python app.py
```
- Flask will start the server on `http://127.0.0.1:5000/chat`
- To test, send a POST request using **Postman** or **curl**:
  ```sh
  curl -X POST http://127.0.0.1:5000/chat -H "Content-Type: application/json" -d '{"message": "Hello!"}'
  ```

### **🔹 Run Command-Line Chatbot (chatbot.py)**
```sh
python chatbot.py
```
- Type your messages to chat with the AI.
- Type `exit` to quit.

---

## 📡 Deploying the Flask API
### **1️⃣ Deploy with Gunicorn (Linux Server)**
```sh
pip install gunicorn
```
Run Flask with Gunicorn:
```sh
gunicorn -w 4 -b 0.0.0.0:5000 app:app
```

### **2️⃣ Deploy on a Cloud Server (Optional)**
To run the API on a **VPS or Cloud**, consider:
- **AWS EC2 / DigitalOcean** (Ubuntu server with `gunicorn` & `nginx`)
- **Heroku** (Deploy Flask as a web service)

---

## 🤖 Telegram Bot Integration
To integrate this chatbot with **Telegram:**
1. **Create a Telegram Bot**
   - Open Telegram & search for `@BotFather`.
   - Type `/newbot` & follow the steps.
   - Get the bot **API Token**.

2. **Install Telegram Library**
   ```sh
   pip install python-telegram-bot
   ```

3. **Create `telegram_bot.py`** with this content:
   ```python
   from telegram import Update
   from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext
   from chatbot import handle_conversation

   TOKEN = "YOUR_TELEGRAM_BOT_TOKEN"

   def start(update: Update, context: CallbackContext):
       update.message.reply_text("Welcome to the AI ChatBot!")

   def chat(update: Update, context: CallbackContext):
       user_input = update.message.text.strip()
       result = handle_conversation(user_input)
       update.message.reply_text(result)

   def main():
       updater = Updater(TOKEN, use_context=True)
       dp = updater.dispatcher
       dp.add_handler(CommandHandler("start", start))
       dp.add_handler(MessageHandler(Filters.text & ~Filters.command, chat))
       updater.start_polling()
       updater.idle()

   if __name__ == "__main__":
       main()
   ```

4. **Run the Telegram Bot**
   ```sh
   python telegram_bot.py
   ```

Now, send messages to your Telegram bot! 🎉

---

## 📝 License
This project is open-source and free to use!

---

## 🙌 Contributing
1. **Fork the repo**
2. **Create a new branch** (`git checkout -b feature-branch`)
3. **Commit changes** (`git commit -m 'Added new feature'`)
4. **Push to GitHub** (`git push origin feature-branch`)
5. **Create a pull request**

---

## 📩 Contact
For any questions, contact **Fares** via email or open an issue on GitHub!

---

**Enjoy your AI-powered chatbot! 🚀🔥**

