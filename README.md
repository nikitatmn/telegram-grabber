# Telegram Grabber v2.2 2024
# Телеграм Граббер v2.2 2024
Бот позволяет пересылать весь контент с любого telegram канала (если админ канала не запретил копирование контента) на ваш канал без упоминания автора канала. Также есть возможность заменить все ссылки и упоминания в постах на ваши

- [x] 02.01.2024 Добавил инлайн-меню, режим модерации, перезагрузку бота из онлайн меню, добавление каналов без команд (по нажатию на инлайн-меню), обновил инструкцию

- [x] 09.01.2024 Добавил возможность добавлять каналы по @username

- [x] 10.01.2024 Задал версию клиента при авторизации для решения возможной проблемы с вылетом на всех устройствах

- [x] 11.01.2024 Фикс отображения встроенных ссылок при замене

- [x] 11.01.2024 Внедрение Chat GPT - в режиме модерации добавил кнопку "Рерайтинг текста" (Работает только с одиночными сообщениями, если отправляется альбом, то кнопки не будет (возможно добавлю в будущем)). Текст по нажатию на кнопку должен будет переписать Chat GPT для создания уникальной публикации.

- [x] 11.01.2024 Теперь все переменные, которые нужно менять, **заполняются в файле config.py**

Планируется:

- [ ] Добавление блэклиста слов для игнорирования рекламных публикаций
      
- [ ] Добавить запрет на обращение к боту не от админа (сейчас к вашим телеграм ботом могут управлять все и видеть ваши каналы)

- [ ] Исправить баг с невозможностью переслать сообщение, если в нём есть превью ссылки

# Используемые библиотеки

_Всё тестировалось на Python 3.11_

Для работы бота необходимо установить библиотеки.

Библиотека aiogram:

    pip install aiogram=2.25.1
_(Если в будущем предложит обновить библиотеку aiogram, то не нужно. Всё работает только на версии 2.25.1)_

Библиотека telethon:   
 
    pip install telethon
_В данный момент всё стабильно работает на последней версии библиотеки telethon (1.33)_

Библиотека pickle:

    pip install pickle

Библиотека httpx: (proxy для работы Chat GPT)

    pip install httpx



# Как запустить

1. Создать телеграм-бота. Для этого нужно написать боту [BotFather](https://telegram.me/botfather) и следовать инструкциям. После этого сохраните токен бота.
2. Получить api_id, api_hash. Сделать это можно на сайте [my.telegram.org](https://my.telegram.org/auth). Инструкция: https://www.youtube.com/watch?v=JBDnmEhvgac
3. Задать переменные api_id, api_hash, bot_token и my_id в файле config.py.

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/610588b4-a6c2-48bf-8e23-229483b8176f)

my_id брать в [Get My ID](https://t.me/getmyid_bot) отсюда (отправить в бот любое сообщение, он выдаст ваш id):

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/10a83730-3708-47d7-a134-f700ef037c4d)



Запустить бота командой:

    python main.py

**При первом запуске нужно ввести номер телефона и код, который придёт в telegram**

# Пример использования:
1. Переходим в telegram бот, который создали в начале. Вводим команду "/start", нажимаем "Добавить канал" и вводим id канала, с которого нужно брать контент. 
id нужного канала можно узнать переслав любое сообщение с канала в бот (пример id для каналов: -1001009232144) [Get My ID](https://t.me/getmyid_bot)
![image](https://user-images.githubusercontent.com/91873172/236866756-06b5a78f-0b58-45f2-a238-ce6e40550b8a.png)

Можно вводить и username через "@", но через id стабильнее работает. **Если через id не получается вводим @username**

2. Добавляем канал, на который должны будут приходить сообщения. Для этого жмём "Добавить канал-получатель". Бот, в котором мы всё это вводим, обязательно должен быть администратором этого канала.
3. Указываем соответсвие между каналами (это нужно, если вы добавите несколько каналов источников и несколько каналов куда публиковать, при этом хотите чтобы публикации из определённых каналов приходили на конкретные каналы) написав id канала-источника и id канала-получателя через пробел командой /set_channel_mapping (Пример: /set_channel_mapping -100123132890 -1000932314321).
4. После этого перезагружаем код либо вручную закрыв и открыв компилятор кода (стабильнее всего), в котором работаем, либо по кнопке "Перезагрузить бота" (не стабильно). **Теперь все новые сообщения будут приходить на ваш канал.**
5. Также вам доступна команда

    /last_messages ко-во сообщений или all, если все
    
Она отправляет последние сообщения на ваш канал. Если добавили несколько каналов-источников, а последние сообщения нужны только с одного канала, то напишите

    /last_messages id канала источника ко-во сообщений

6. Режим модерации. При активации режима модерации все сообщения будут приходить сначала на ваш технический канал, в котором вы можете их редактировать, удалять и публиковать:

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/cbdf1fb7-e5b0-4870-b01a-59a514785abd)


![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/da314d89-fc1f-4d48-885b-d801ed31df1c)

Для его работы создаём новый пустой канал и вводим id этого канала в technical_channel_id в файле config.py. (получить id можно по аналогии как с остальными каналами). Не забываем назначить бота администратором технического канала.

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/a9ad67b1-2cc2-4967-9519-59a6e458588e)

Если вы отредактировали сообщение, то нажимайте на "Отредактировано" чтобы оно обновилось в хранилище. Возможный баг: когда в техническом канале скапливается большое количество сообщений, то при нажатии на "Отправить" может зависать. Чтобы всё заработало нажимаем на "Отредактировано", а потом "Отправить".

**Также есть возможность заменять все ссылки и упоминания, которые публикуются на каналах на ваши**. В файле config.py замените на нужные вам

![image](https://github.com/WALTERXO/telegram-grabber/assets/91873172/ac6f8843-372a-4d73-8c1d-09c4a36aa491)

**Рерайт текста с Chat GPT**. В режиме модерации есть кнопка "Рерайт текста". Для её работы заполняем proxy_url и openai_api_key в файле config.py. proxy_url должны быть формата HTTP или HTTPS. Если у вас прокси с логином и паролем, то в настройках прокси ставьте авторизацию по вашему ip. openai_api_key берётся на сайте openai https://platform.openai.com/api-keys приналичии бюджета в https://platform.openai.com/usage . При отсутствии прокси и openai_api_key за покупкой можно обратиться ко мне.



# Список доступных команд:
* /start - Начало работы с ботом
* /help - Получить список доступных команд
* /add_channel - Добавить канал для работы
* /remove_channel - Удалить канал из списка
* /list_channels - Показать список добавленных каналов
* /add_destination_channel - Добавить канал-получатель
* /remove_destination_channel - Удалить канал-получатель из списка
* /list_destination_channels - Показать список каналов-получателей
* /set_channel_mapping - Установить соответствие между каналами
* /last_messages (ко-во сообщений или all, если все) - Отправить последние сообщения с каналов


Списки идентификаторов каналов хранятся в файле *.pickle для сохранения настроек после перезапуска бота. Отправка сообщений из технического после перезагрузки бота, когда модерация включена, слетит.



