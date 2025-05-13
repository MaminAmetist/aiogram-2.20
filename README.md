# Weather Telegram Bot

Telegram-бот для мониторинга погоды на Python. Этот проект представляет собой простого Telegram-бота, который предоставляет текущую погоду по названию города. Пользователи могут отправить команду `/start` для приветствия и затем ввести название города, чтобы получить сводку погоды.

## Описание

Бот использует API OpenWeatherMap для получения данных о погоде и библиотеку `aiogram` для взаимодействия с Telegram API. Он отвечает на команды и сообщения, предоставляя информацию о текущей погоде, включая температуру, влажность, давление, скорость ветра, а также время восхода и заката солнца.

## Установка

1. **Клонируйте репозиторий или скачайте исходный код**

```bash
git clone https://github.com/yourusername/weather-telegram-bot.git
cd weather-telegram-bot
```

2. **Создайте виртуальное окружение (опционально)**

```bash
python -m venv venv
source venv/bin/activate  # для Linux/MacOS
venv\Scripts\activate     # для Windows
```

3. **Установите необходимые библиотеки**

```bash
pip install aiogram requests
```

4. **Настройте API ключи**

- Получите токен вашего бота у [BotFather](https://t.me/BotFather) в Telegram и вставьте его вместо `'my_token'` в файле.
- Получите API ключ OpenWeatherMap на [официальном сайте](https://openweathermap.org/api) и вставьте его вместо `'your_open_weather_key'`.

5. **Запустите бота**

```bash
python bot.py
```

## Конфигурация

В файле `bot.py` необходимо заменить:

```python
bot = Bot(token='my_token')  # Токен вашего Telegram бота
```

и

```python
response = requests.get(
    f"http://api.openweathermap.org/data/2.5/weather?q=москва&lang=ru&units=metric&appid=your_open_weather_key"
)
```

на актуальные значения.

---

## Использование

1. Откройте чат с ботом в Telegram.
2. Отправьте команду `/start` — бот поприветствует вас.
3. Введите название города (например, `Москва`, `Санкт-Петербург`, `Киев`) — бот пришлет текущую погоду.

**Пример:**

```
Москва
```

**Ответ:**

```
2023-10-15 14:30
Погода в городе: Москва
Температура: 10°C ☀️
Влажность: 70%
Давление: 760 мм.рт.ст
Ветер: 3 м/с 
Восход солнца: 2023-10-15 07:00:00
Закат солнца: 2023-10-15 18:30:00
Продолжительность дня: 11:30:00
Хорошего дня!
```

---

## Важные замечания

- В текущей реализации бот всегда запрашивает погоду для города "Москва". Чтобы сделать его динамическим по введённому пользователем названию города, нужно изменить код функции `get_weather`, чтобы использовать текст сообщения как название города.

Пример изменения:

```python
@dp.message_handler()
async def get_weather(message: types.Message):
    city_name = message.text.strip()
    try:
        response = requests.get(
            f"http://api.openweathermap.org/data/2.5/weather?q={city_name}&lang=ru&units=metric&appid=your_open_weather_key"
        )
        # остальной код...
```

---

**Примечание:** Не забудьте заменить все заглушки (`'my_token'`, `'your_open_weather_key'`) на реальные значения перед запуском!
