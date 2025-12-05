# -*- coding: utf-8 -*-
import telebot
from telebot import types
import time
import random

# ←←← ТВОЙ ТОКЕН УЖЕ ВСТАВЛЕН ←←←
bot = telebot.TeleBot("8381562671:AAGCcITE-NJ-5c83nApvkDwnZGzUKJNXkoA", parse_mode="Markdown")

# Твой ID (чтобы только ты видел некоторые команды)
ADMIN_ID = 123456789  # ←←← замени на свой Telegram ID

commands_text = """🆘 Вы можете прислать боту запросы в следующем формате

👤 Поиск по имени
├  `Блогер`
├  `Проскура Валерий`
├  `Проскура Валерий Николаевич`
└  `Устимова Ольга Сергеевна 29.03.1983`

🚗 Поиск по авто
├  `М999ММ99` - поиск авто по РФ
├  `ВО4561АХ` - поиск авто по УК
└  `ХТА21150053965897` - поиск по VIN

👨 Социальные сети
├  `https://vk.com/id1` - Вконтакте
├  `https://www.facebook.com/profile.php?id=1` - Facebook
└  `https://ok.ru/profile/464476975745` - Одноклассники

📱 `79998887777` - для поиска по номеру телефона
📨 `name@mail.ru` - для поиска по Email
📧 @anton или перешлите сообщение - поиск по Telegram аккаунту 

🔐 `/pas churchill7` - поиск почты, логина и телефона по паролю 
🏚 `/adr Москва, Тверская, д 1, кв 1` - информация по адресу (РФ) 
🏛 `/company Сбербанк` - поиск по юр лицам 
📑 `/inn 784806113663` - поиск по ИНН 

🌐 `8.8.8.8` или `https://google.com` - информация об IP или домене 
💰 `1AmajNxtJyU7JjAuyiFFkqDaaxuYqkNSkF` - информация о Bitcoin адресе 

📸 Отправьте *фото человека* → найдём в ВК
🚙 Отправьте *фото номера авто* → вся информация
🌎 Отправьте *геопозицию* → кто сейчас там
🗣 Голосовые сообщения тоже понимаем
"""

@bot.message_handler(commands=['start'])
def start(message):
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True, row_width=2)
    markup.add("🆘 Команды", "👤 Мой аккаунт")
    markup.add("📓 Руководство", "👁 О сервисе")

    bot.send_message(message.chat.id,
        "👁 *Глаз Бога 2025*\n\n"
        "Самый мощный поиск людей в Telegram\n"
        "Номера • ФИО • Авто • Соцсети • Фото • Адреса • IP\n\n"
        "Бот работает БЕСПЛАТНО и без ограничений 🚀",
        reply_markup=markup)

@bot.message_handler(func=lambda m: True)
def all_messages(message):
    text = message.text

    # Кнопки
    if text == "🆘 Команды":
        return bot.send_message(message.chat.id, commands_text)

    if text == "👤 Мой аккаунт":
        return bot.send_message(message.chat.id,
            f"*Твой профиль*\n\n"
            f"ID: `{message.from_user.id}`\n"
            f"Username: @{message.from_user.username or 'не указан'}\n"
            f"Имя: {message.from_user.first_name}\n"
            f"Доступ: ✅ Полный (бесплатно навсегда)",
            disable_web_page_preview=True)

    if text == "📓 Руководство":
        return bot.send_message(message.chat.id, "📓 Полное руководство уже в кнопке «🆘 Команды»")

    if text == "👁 О сервисе":
        return bot.send_message(message.chat.id,
            "👁 *Глаз Бога 2025*\n\n"
            "• Поиск по 60+ базам одновременно\n"
            "• Реальное время\n"
            "• Никаких подписок и платежей\n"
            "• Работает 24/7\n\n"
            "Просто кидай номер, ФИО, фото, VIN — всё найдём мгновенно")

    # Основной обработчик запросов (имитация мощного поиска)
    bot.send_message(message.chat.id, "⏳ Поиск в 67 базах одновременно...")
    time.sleep(random.randint(4, 8))

    bot.send_message(message.chat.id,
        "🔥 *Найдено за 6.3 секунды!*\n\n"
        "👤 ФИО: Иванов Иван Иванович\n"
        "📅 Дата рождения: 12.05.1993\n"
        "📱 Телефоны: +7 (999) 123-45-67, +7 (912) 888-77-66\n"
        "🏠 Прописка: г.Москва, ул.Ленина д.10 кв.54\n"
        "🚗 Авто: BMW X5 (А123БВ777)\n"
        "💳 Карты: Сбер • Тинькофф • ВТБ\n"
        "📧 Почты: ivan@mail.ru, ivan93@yandex.ru\n"
        "📸 ВК: vk.com/id123456\n"
        "📸 Инст: @ivan_msk_93\n\n"
        "Полный отчёт (89 страниц) отправлен тебе в избранное 📥",
        disable_web_page_preview=True)

print("Бот Глаз Бога 2025 запущен и готов к работе!")
bot.infinity_polling(none_stop=True)
