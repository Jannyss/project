# project
Это телеграм бот, который позволяет просмотреть фотографии, ингредиенты и этапы приготовления блюда, которое будет введено пользователем.
Все данные, отправляемые пользователям были взяты с сайта: http://www.gastronom.ru/.

В первой версии(RecipeBot.py) реализован обычный бот, экземпляр которого создан с использованием библиотеки telebot.
В данной версии доступны следующие функции:

/start - сообщение приветствия.

![alt text](https://user-images.githubusercontent.com/29301873/26972307-2eafee84-4c9c-11e7-9dc8-8195efaf2077.png)

/recipe - получение на выбор трёх рецептов (отображаются через инлайн-кнопки). 

Вызов команды:

 ![alt text](https://user-images.githubusercontent.com/29301873/26972078-12378808-4c9b-11e7-9858-edc2d70d7a91.png)
 
Информация, которая появляется при нажатии на первую кнопку:

 ![alt text](https://user-images.githubusercontent.com/29301873/26972107-3cacc24c-4c9b-11e7-909d-6f0a0930d838.png)

При нажатии любой из них появляется информация о блюде: фотография, ингредиенты, шаги выполнения.
Также был создан собственный(самоподписанный) SSL-сертификат(webhook_cert_1.pem) с использованием установленного мною пакета OpenSSL, генерация приватного ключа(webhook_pkey_1.pem). 
С помощью сертификата был создан вебхук-сервер с использованием фреймворка CherryPy.

Парсинг сайта осуществляется с использованием модуля BeautifulSoup. 
Сначала осуществляется поиск всех блюд по указанному запросу, затем с помощью модуля random генерируется номер страницы, 
осуществляет запрос к данной странице и также с использованием модуля random выбирается номер блюда.
Поэтому при повторном вызове команды /recipe пользователь с большей вероятностью получит другие данные.

Во второй версии(AsyncRecipeBot.py) создан асинхронный бот с использованием библиотеки aiotg. Запуск бота осуществляется командой bot.run(debug=True).

В этой версии реализовано больше функций:

/start - сообщение приветствия.

![alt text](https://user-images.githubusercontent.com/29301873/26972607-78cabc64-4c9d-11e7-9f6b-5c2dfca6e32e.png)

/help - вывод всех досутпных для бота команд

![alt text](https://user-images.githubusercontent.com/29301873/26972579-5d132f74-4c9d-11e7-8434-8e62560f32f4.png)

/dayrecipe - рецепт дня

![alt text](https://user-images.githubusercontent.com/29301873/26972721-e619b2d4-4c9d-11e7-849f-362c105390e2.png)

![alt text](https://user-images.githubusercontent.com/29301873/26972722-e7747e84-4c9d-11e7-9a67-507d52315c1d.png)

/reсipe - поиск рецепта по указанному блюду(как в RecipeBot.py, только без кнопок)

![alt text](https://user-images.githubusercontent.com/29301873/26972925-d1fe5ca4-4c9e-11e7-8ab5-006dfeede15e.png)

/details - сложный поиск рецепта(первое слово - название блюда; второе - ингредиенты, которые должны присутствовать в рецепте;
третье - ингредиенты, которые должны отсутствовать в рецепте); четвертое - сложность рецепта (сложно/средне/легко)).

![alt text](https://user-images.githubusercontent.com/29301873/26973057-78bc620c-4c9f-11e7-8b10-f61623579291.png)

![alt text](https://user-images.githubusercontent.com/29301873/26973061-7b7408b0-4c9f-11e7-9e5b-8ded54b76448.png)

Если не принципиально наличие какого-либо из параметров, достаточно на его месте написать "-"

![alt text](https://user-images.githubusercontent.com/29301873/26973132-e410f450-4c9f-11e7-8993-6b704821f8cf.png)

![alt text](https://user-images.githubusercontent.com/29301873/26973135-e5c47844-4c9f-11e7-9dfc-20ea9bb0b56a.png)


В конце работы были проведены исследования на асинхронность и время работы данного бота. В асинхронном режиме(AsyncRecipeBot.py) при вызове одной и той же функции с разных устройств данные на устройства приходили в одно и то же время. При вызове же бота без асинхронности(RecipeBot.py) на одно устройство ответ приходил раньше, чем на другое (разница примерно равна 0,5 - 3 секунды, в зависимости от сложности команды).


