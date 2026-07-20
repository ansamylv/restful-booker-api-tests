| ID | Проверка | Ожидаемый результат | Фактический результат | Статус |
| :--- | :--- | :--- | :--- | :---: |
| **AUTH** | **POST /auth (Создание токена)** | | | |
| `AUTH-01` | Успешная генерация токена | `200 OK`, тело ответа содержит ключ `"token"` | `200 OK`, `{"token": "0c032d0455ed411"}` |  Pass |
| `AUTH-02` | Невалидный пароль в Request Body | `200 OK`, тело ответа: `{"reason": "Bad credentials"}` | `200 OK`, `{"reason": "Bad credentials"}` |  Pass |
| `AUTH-03` | Невалидный юзернейм в Request Body | `200 OK`, тело ответа: `{"reason": "Bad credentials"}` | `200 OK`, `{"reason": "Bad credentials"}` |  Pass |
| `AUTH-04` | Передача пустого JSON `{}` в Request Body | `200 OK`, тело ответа: `{"reason": "Bad credentials"}` | `200 OK`, `{"reason": "Bad credentials"}` |  Pass |
