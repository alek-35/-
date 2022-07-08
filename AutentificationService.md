# Autentification Service
## Точки входа:
1. /login
2. /logout
3. /refresh
4. /validate
5. /user

## /login (POST)
Используется для начала сессии пользователя
На вход поступает
```
{
    "login":"user_login",
    "password":"user_hashed_password"
}
```
На выходе если логин/пароль верный получаем объект:
```
{
    "access_token":"ffdvgv",
    "refresh_token":"ftevrtxyh",
    "valid_until":"03-07-22 19:50"
}
```
В противном случае - ошибка.

## /logout (POST)
Используется для завершения сессии пользователя
На вход поступает
```
{
    "access_token":"ffdvgv",
    "refresh_token":"ftevrtxyh",
}
```
Далее пользователь теряет возможность пользоваться этими токенами

## /refresh (POST)
Используется для продления сессии пользователя
На вход поступает:
```
{
    "access_token":"ffdvgv",
    "refresh_token":"ftevrtxyh",
}
```
В ответ получаем
```
{
    "refresh_token":"ftevrtxyh",
    "valid_until":"03-07-22 20:50"
}
```
## /validate (POST)
Используется для проверки токена пользователя пользователя и получения его полномочий
На вход поступает:
```
{
    "access_token":"ffdvgv",
    "refresh_token":"ftevrtxyh",
}
```
В ответ получаем
```
{
    "scopes":[
        "storage"
    ]
}
```
## /user (GET,POST,PATCH,DELETE)
### GET
Получение списка пользователей системы
В ответ приходит
```
{
    "users":[
        {
            "id":"id",
            "name":"Иванов И.И",
            "email":"test@com",
            "phone":"123455678",
            "scopes":[
                "storage"
            ]
        }
    ],
    "total":10
}
```
### POST
Добавление пользователя системы
На вход отправляем
```
{
    "name":"Иванов И.И",
    "login":"test_login",
    "password":"password",
    "email":"test@com",
    "phone":"123455678",
    "scopes":[
        "storage"
    ]
}
```

### PATCH
Обнвление данных пользователя системы
На вход отправляем
```
{
    "name":"Иванов И.И",
    "login":"test_login",
    "password":"password",
    "email":"test@com",
    "phone":"123455678",
    "scopes":[
        "storage"
    ]
}
```

### DELETE
Удаление пользователя
На вход отправляем
```
{
    "id":"uuid",
}
```

## Схема БД
Таблица пользователей
| user_id     | login       | password | name | email | phone | scopes|
| ----------- | ----------- | ----     | ---- | ----- | ----- | ----- |
| aabf-sccfsc | boomer      | csfcvdfv | test | t@com | +1234 | assdf |

Таблица прав ппользователей
| user_id     | id          | scope1   | scope2 | scope3 | 
| ----------- | ----------- | ----     | ----   | -----  |
| aabf-sccfsc | aassdd      | 1        | 0      | 1      |