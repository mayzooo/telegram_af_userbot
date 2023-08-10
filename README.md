How to get started:
Download the bot
In the "tg_config.py" file, replace all data with your own (api_id, api_hash, bot_token, admin_id)
Run the bot via the "main.py" file
After launch, go to the bot and log in to your Telegram account (in version 1.0.0.0 beta, authorization with a cloud password is not available, turn it off at the time of authorization)
After authorization, go to Telegram settings, select the session of the bot from which you entered Telegram and turn off the ability for this session to receive calls and secret chats

Implemented features:
- (NEW!) Authorization through the bot itself (if a cloud password is set, it must be disabled during authorization)
- (NEW!) Multi-account - one control panel for several users
- Control panel via Telegram bot
- Navigate through bot buttons without using commands other than /start
- Saving and loading settings from/to the SQLite database
- Add/remove a user to a shipment
- The ability to freeze/unfreeze the shipment of an individual user independently of others
- Ability to start/stop forwarding of all users (globally, freezing/unfreezing of forwarding separately by user remains unchanged)
- Ability to disable/enable forwarding of your messages in chat with added users
- Displaying a list of all added shipments for each user with their activity statuses
- Forwarding messages from users to your private channel
- Add to shipment through:
- - Sending a user's contact from their Telegram profile
- - Select an existing chat with the user
- - Selecting a synchronized user contact in Telegram
- - Adding through a user's forwarded message, if he does not have an active item in his privacy settings to hide the link to his account when forwarding a message
- When adding to the shipment, it is possible to:
- - Automatically create a new channel (a private channel is created)
- - Choose an existing one (private channel, the creator of which you are)
- The ability to change the channel to which messages are forwarded (the same choice that is provided when adding a user to forwarding)
- Deleting a user from forwarding (the channel where messages were forwarded is saved)
- Full wipe of message forwarding settings with their channels (irreversible action)
- Forwarding types of messages:
- - Text
- - Photos (including burnt ones)
- - Videos (including burned ones)
- - Video message (those circles :))
- - Voice messages
- - Geoposition (not to be confused with a beacon)
- - Forwarded messages both from other users and from channels
- - Stickers
- - Gifs
- - Files
- - Media group (there is a nuance, look in possible problems)
- Online status does not change (invisible, see the explanation in the "possible problems" section)
- The status of reading messages does not change, including for burning photos/videos

Possible problems:
- A group of media is forwarded in one file, but it is one message - Yes, this is such a feature, for some reason the Pyrogram library sees them as separate messages, and there are problems with this due to flooding, I have not solved it yet, so the console will throw a message about repeated attempts to send via 2 seconds.
- If a group of forwarded messages arrives, they are forwarded one at a time and with a delay - Yes, this is each individual message, so the situation is the same as with grouped media above.
- About online status and redundant notifications - Forwarding of messages is implemented through delayed messages with a timer of one minute (can be configured in the file "user_processor.py" -> class UserMessages -> forward_processor -> date -> minutes=1). This is due to the fact that the "online" status is activated for you during a direct transfer. This is not my whim, this is the implemented mechanism of Telegram itself. Also, although snoozed messages are published with a "do not notify" status, you will receive notifications. This is partially remedied by turning off notifications from the channel. Why partially? On the phone (at least with the Android OS), notifications stop going after this, but pop-up notifications remain in the Telegram client for PC, because this is how the Telegram client is arranged.
- The user edited the message, but it has not changed in forwarded messages - Of course, this is how forwarded messages work, try to forward your message yourself and then edit it and compare. Instead, the bot forwards them as soon as they arrive (with the possible exception of the media group and forwarded message group).

RU
Юзербот (тот который авторизуется как приложение в вашем Телеграмм аккаунт, не путать с обычным ботом в Телеграмм) для автоматических пересылок личных сообщений от пользователей
Базируется на библиотеке "Pyrogram"

Предыстория:
Меня задолбали мои контакты, которые пишут и удаляют сообщения до того, как я их прочитал, поэтому я создал бота, который будет автоматически пересылать сообщения от необходимых пользователей в отдельный канал, где я в случае удаления смогу их спокойно прочитать.

Предупреждение!
Вы используете его на свой страх и риск, я не несу никакой ответственности и не принимаю претензии за какие-либо возможные последствия при использовании этого бота (как вот возможен бан вашего аккаунта в телеграммах)! Используя этот бот вы подтверждаете то, что вы знаете что делаете и к каким последствиям это может привести!

Как начать:
Загрузи бота
В файле "tg_config.py" замени все данные на свои (api_id, api_hash, bot_token, admin_id)
Запусти бота через файл "main.py"
После запуска перейди в бота и авторизуйся в свой телеграмм аккаунт (в версии 1.0.0.0 beta авторизация с облачным паролем недоступна, на момент авторизации выключи ее)
После авторизации зайди в настройку телеграмм, выбери сессию бота из которого ты зашел в телеграмм и выключи возможность этой сессии получать звонки и секретные чаты

Фичи, которые реализованы:
- (NEW!) Авторизация через самого бота (если установлен облачный пароль, то его нужно выключить на время авторизации)
- (NEW!) Мультиаккаунт – одна панель управления для нескольких пользователей
- панель управления через телеграмм бота
- Навигация через кнопки бота не используя команды, кроме как /start
- Сохранение и загрузка настроек с/у базы данных SQLite
- Добавление/удаление пользователя в пересылку
- возможность заморозить/разморозить пересылку отдельного пользователя независимо от других
- Возможность запустить/остановить пересылку всех пользователей (глобально, заморозка/разморозка пересылки отдельно по пользователю остаются неизменными)
- Возможность отключить/включить пересылку сообщений в чате с добавленными пользователями
- вывод списка всех добавленных пересылок по каждому пользователю с их статусами активности
- Пересылка сообщений от пользователей в свой приватный канал
- добавление в пересылку через:
- - Отправка контакта пользователя из его профиля Телеграмм
- - Выбор имеющегося чата с пользователем
- - Выбор синхронизированного контакта пользователя в телеграммах
- - Добавление через пересланное сообщение пользователя, если у него в настройках конфиденциальности не активный пункт скрытия ссылки на его аккаунт при пересылке сообщения
- при добавлении в пересылку есть возможность:
- - автоматически создать новый канал (создается частный канал)
- - Выбрать уже имеющийся (частный канал, создателем которого являешься ты)
- возможность изменить канал куда пересылаются сообщения (тот же выбор, который предоставляется при добавлении пользователя в пересылку)
- удаление пользователя с пересылки (канал куда пересылаемые сообщения сохраняется)
- Полный вайп настроек пересылки сообщений с их каналами (необратимое действие)
- Пересылка типов сообщений:
- - Текст
- - Фото (в том числе сгораемые)
- - Видео (в том числе сгораемые)
- - Видео сообщения (те кружочки :))
- - Голосовые сообщения
- - геопозиция (не путать с маячком)
- - Пересланные сообщения как от других пользователей, так и с каналов
- - Стикеры
- - Гифки
- - Файлы
- - Группа медиа (есть нюанс, смотри в возможных проблемах)
- Статус онлайн не меняется (невидимка, пояснения смотри в пункте "возможные проблемы")
- Статус прочтения сообщений не меняется, в том числе и для сгораемых фото/видео

Возможные проблемы:
- Группа медиа пересылается по одному файлу, но она является одним сообщением - Так это такая фича почему-то библиотека Pyrogram видит их как отдельные сообщения, и с этим есть проблемы по флуду, еще не решил ее поэтому в консоль будет бросать сообщение о повторной попытке отправки через 2 секунды.
- Если поступает группа пересланных сообщений они пересылаются по одному и с задержкой. - Да, это каждое отдельное сообщение, поэтому ситуация такая же как с группированными медиа выше.
- О статусе онлайн и лишних оповещениях - Пересылка сообщений реализована через отложенные сообщения с таймером в одну минуту (можно настроить в файле "user_processor.py" -> class UserMessages -> forward_processor -> date -> minutes=1). Это связано с тем, что при прямой пересылке у тебя активируется статус "онлайн". Это не моя прихоть, так реализован механизм самого телеграммы. Также, хотя отложенные сообщения публикуются со статусом "не оповещать" тебе будут приходить уведомления. Частично это лечится отключением извещений от канала. Почему отчасти? На телефоне (по крайней мере с ОС Андроид) после этого уведомления перестают идти, но в телеграммах клиенты для ПК всплывающие уведомления останутся, так устроен телеграмм клиент.
– Пользователь отредактировал сообщение, а у пересланных оно не изменилось – Конечно, так работают пересланное сообщение, попробуй сам переслать свое сообщение а затем отредактировать его и сравнить. Тем более бот пересылает их сразу когда они приходят (возможно исключение группы медиа и группы пересланных сообщений).
