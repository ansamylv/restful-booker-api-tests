### POST /auth (Создание токена)

| ID | Проверка | Ожидаемый результат | Фактический результат | Статус |
| :--- | :--- | :--- | :--- | :---: |
| **AUTH-01** | Успешная генерация токена | 200 OK, тело ответа содержит ключ "token" | 200 OK, {<br>    "token": "0c032d0455ed411"<br>} |  **Pass** |
| **AUTH-02** | Невалидный пароль в Request Body | 200 OK, тело ответа: {"reason": "Bad credentials"} | 200 OK, {<br>    "reason": "Bad credentials"<br>} |  **Pass** |
| **AUTH-03** | Невалидный юзернейм в Request Body | 200 OK, тело ответа: {"reason": "Bad credentials"} | 200 OK, {<br>    "reason": "Bad credentials"<br>} |  **Pass** |
| **AUTH-04** | Передача пустого JSON {} в  Request Body | 200 OK, тело ответа: {"reason": "Bad credentials"} | 200 OK, {<br>    "reason": "Bad credentials"<br>} |  **Pass** |

### /booking (Управление бронированиями)

| ID | Проверка | Ожидаемый результат | Фактический результат | Статус |
| :--- | :--- | :--- | :--- | :---: |
| **BOOK-01** | Запрос всех бронирований без параметров | 200 ОК, тело ответа содержит значение: ключ<br>"bookingid" : id | 200 OK,<br>[<br>    {<br>        "bookingid": 1<br>    },<br>    {<br>        "bookingid": 2<br>    }, ... |  **Pass** |
| **BOOK-02** | Запрос всех бронирований с фильтром:<br>по имени | 200 OK, тело ответа содержит значение: ключ <br>"bookingid" : id | 200 OK, [<br>    {<br>        "bookingid": 12<br>    },<br>    {<br>        "bookingid": 17<br>    },<br>    {<br>        "bookingid": 25<br>    }, ... |  **Pass** |
| **BOOK-03** | Запрос всех бронирований с фильтром:<br>по дате | 200 OK, тело ответа содержит значение: ключ <br>"bookingid" : id | 200 ОК, выводит пустой массив <br>[] <br>с одновременно введеными <br>параметрами checkin и checkout |  **Fail** |
| **BOOK-04** | Поиск несуществующего имени  | 200 ОК, возвращает пустой массив [] | 200 OK, выводит пустой массив |  **Pass** |
| **BOOK-05** | Получить информацию о конкретном <br>бронировании при валидном id | 200 OK, тело содержит все значения: <br>firstname              <br>lastname        <br>totalprice        <br>depositpaid        <br>bookingdates<br>  checkin                <br>  checkout                <br>additionalneeds (необяз) | 200 ОК, корректно выводит <br>все значения |  **Pass** |
| **BOOK-06** | Получить информацию о конкретном <br>бронировании при невалидном id <br>(<0) | 404 Not Found <br>или<br>400 Bad Request | 404 Not Found |  **Pass** |
| **BOOK-07** | Получить информацию о конкретном <br>бронировании при невалидном id <br>(=0) | 404 Not Found <br>или<br>400 Bad Request | 404 Not Found |  **Pass** |
| **BOOK-08** | Передать все данные для создания <br>бронирования | 200 ОК, тело ответа содержит все значениия: <br>bookingid<br>booking<br>firstname<br>lastname<br>totalprice<br>depositpaid<br>bookingdates<br>checkin<br>checkout<br>additionalneeds | 200 ОК, тело ответа содержит <br>все соответствующие значения |  **Pass** |
| **BOOK-09** | Передать значения без поля firsname | 404 Not Found <br>или<br>400 Bad Request | 500 Interval Server Error |  **Fail** |
| **BOOK-10** | Обновление текущего бронирования  | 200 ОК, тело ответа содержит все значения как <br>в BOOK-05<br>Данные обновлены | 200 ОК,  тело ответа содержит <br>все соответствующие значения<br>Данные обновлены |  **Pass** |
| **BOOK-11** | Обновление текущего бронирования с <br>пустым полем firsname | 404 Not Found <br>или<br>400 Bad Request | 400 Bad Request |  **Pass** |
| **BOOK-12** | Частичное обновление: firstname и lastname | 200 OK, поля firstname и lastname обновлены <br>тело ответа содержит все значения как в BOOK-05 | 200 ОК, firstname и lastname <br>обновлены<br>тело содержит все соотв. значения |  **Pass** |
| **BOOK-13** | Частичное обновление: firstname | 200 OK, поле firstname  обновлено тело ответа<br> содержит все значения как в BOOK-05 | 200 OK, firstname обновлен, тело <br>ответа содержит все соотв. значения |  **Pass** |
| **BOOK-14** | Частичное обновление с невалидным id (-1) | 404 Not Found <br>или<br>400 Bad Request | 405 Method Not Allowed |  **Fail** |
| **BOOK-15** | Удаление брони с валидным id | 201 Created | 201 Created |  **Pass** |
| **BOOK-16** | Удаление брони с невалидным id<br>(-1) | 404 Not Found <br>или<br>400 Bad Request | 405 Method Not Allowed |  **Fail** |

### GET /ping (Проверка состояния)

| ID | Проверка | Ожидаемый результат | Фактический результат | Статус |
| :--- | :--- | :--- | :--- | :---: |
| **PING-01** | Проверка состояния | 201 Created | 201 Created |  **Pass** |