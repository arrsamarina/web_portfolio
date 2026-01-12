---
title: "Протокол HTTP. Клиент–серверное взаимодействие"
date: 2026-01-03T17:30:00+03:00
draft: false
type: "reports"
weight: 3
---

## Цель работы
Изучить основы клиент–серверного взаимодействия по протоколу HTTP, структуру HTTP-запросов и ответов, а также освоить отправку GET и POST запросов с использованием CLI-утилит и GUI-инструментов.

---

## 1. Отправка HTTP-запросов через Telnet (CLI)

Для демонстрации работы с, так скажем, «сырым» HTTP-протоколом была использована утилита **telnet**, позволяющая вручную формировать HTTP-запросы и получать ответы сервера.

### GET-запрос через Telnet

Подключение к серверу:

telnet httpbin.org 80

Отправленный HTTP-запрос:

GET /get HTTP/1.1
Host: httpbin.org
Connection: close

Сервер вернул корректный ответ со статусом `HTTP/1.1 200 OK`, HTTP-заголовками и телом ответа в формате JSON.

![GET через telnet](../images/telnet-get.jpg)
![GET через telnet](../images/telnet-get.jpg)

---

### POST-запрос через Telnet

Отправленный HTTP-запрос:

POST /post HTTP/1.1
Host: httpbin.org
Content-Type: application/json
Content-Length: 29
Connection: close

{"name":"Arina","lab":"HTTP"}


Сервер успешно принял POST-запрос и вернул статус `200 OK`. В теле ответа отображены переданные данные в формате JSON.

![POST через telnet](../images/telnet-post.jpg)
![POST через telnet](../images/telnet-postt.jpg)

---

## 2. Отправка HTTP-запросов с помощью cURL

### Проверка установки cURL

Для начала была проверена установленная версия cURL:

curl.exe --version

![curl version](../images/curl-version.jpg)

---

### GET-запрос через cURL

Отправка GET-запроса:

curl.exe https://httpbin.org/get


Сервер вернул JSON-ответ с параметрами запроса, заголовками и информацией о клиенте.

![GET через curl](../images/curl-get.jpg)

---

### POST-запрос через cURL

Для передачи JSON-данных был выполнен POST-запрос:

curl.exe -X POST https://httpbin.org/post

-H "Content-Type: application/json"
-d '{"name":"Arina","lab":"HTTP"}'


Сервер корректно обработал JSON-тело запроса и вернул его в поле `json` ответа.

![POST через curl](../images/curl-post.jpg)

---

## 3. Использование GUI-инструмента Postman и API Банка России

Для отправки HTTP-запросов с использованием графического интерфейса был выбран инструмент **Postman**.

### GET-запрос к API Банка России

Используемый URL:

https://www.cbr.ru/scripts/XML_dynamic.asp


Query-параметры:
- `date_req1 = 01/01/2024`
- `date_req2 = 10/01/2024`
- `VAL_NM_RQ = R01235` (доллар США)

В ответ сервер Банка России вернул корректный XML-документ с курсом валюты за выбранный период.

![Postman + API ЦБ РФ](../images/postman-cbr.jpg)

---

## Вывод

В ходе выполнения лабораторной работы были изучены основы протокола HTTP и принципы клиент–серверного взаимодействия. Были успешно отправлены GET и POST запросы с использованием утилит telnet и cURL, а также выполнен запрос к публичному API Банка России с помощью GUI-инструмента Postman. Полученные результаты подтверждают корректную работу HTTP-запросов и.. приемлемое понимание структуры HTTP-сообщений.
