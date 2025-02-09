import os
import logging
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters, CallbackContext

# Включаем логирование
logging.basicConfig(
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s", level=logging.INFO
)

TOKEN = os.getenv("BOT_TOKEN")

# Функция для команды /start
async def start(update: Update, context: CallbackContext) -> None:
    await update.message.reply_text("Привет! Я ваш AI учитель по химии. Задавайте вопросы!")

# Обработчик текстовых сообщений
async def handle_message(update: Update, context: CallbackContext) -> None:
    user_text = update.message.text
    await update.message.reply_text(f"Вы спросили: {user_text}. Я пока учусь отвечать!")

def main():
    app = Application.builder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

    app.run_polling()

if __name__ == "__main__":
    main()
