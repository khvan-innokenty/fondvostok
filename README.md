# fondvostok

Формат обмена данными - **JSON**\
Кодировка - **UTF-8**

## POST Создание нового участка
Поля запроса:
1. **id** - идентификатор участка, уникальная строка
2. **coords** - массив координат в градусах с точностью 6 точек после запятой
3. **area** - площадь участка в гектарах с точностью 2 точки после запятой
4. *формируются*

Пример POST-запроса:
```json
{
   "id": "1234567890ABCD",
   "coords":[
      {
         "lat": 43.406667,
         "lng": 134.895467
      },
      {
         "lat": 43.419250,
         "lng": 134.932517
      },
      {
         "lat": 43.413717,
         "lng": 134.937050
      },
      {
         "lat": 43.400583,
         "lng": 134.898900
      }
   ],
   "area": 242.71
}
```

Ожидаемый ответ:
1. **code** - число, ответ сервера ([возможные ответы](https://github.com/khvan-innokenty/fondvostok/blob/master/CODES.md#Коды-ответов-сервера-на-запрос-создания-участка))
2. **message** - расшифровка ответа сервера 
3. **id** - идентификатор участка, уникальная строка
4. **timestamp** - временная метка обработки запроса
5. *формируются*

Пример ответа:
```json
{
   "code": 202,
   "message": "Запрос принят в обработку",
   "id": "1234567890ABCD",
   "timestamp": 1496411085
}
```

## GET Получение информации об участках
Поля запроса:
1. **id** - массив идентификаторов участков.

Пример GET-запроса для нескольких участков:
```json
{
   "id": [
   "1234567890ABCD",
   "1234567890ABCX"
   ]
}
```

Ожидаемый ответ:
1. **code** - число, статус участка ([возможные статусы](https://github.com/khvan-innokenty/fondvostok/blob/master/CODES.md#Статусы-участков))
2. **message** - расшифровка статуса
3. **id** - идентификатор участка, уникальная строка
4. **timestamp** - временная метка обработки запроса
5. **data** - дополнительные данные, формат зависит от ответа сервера **code**
6. *формируются*

Пример ответа:
```json
[
   {
      "code": 601,
      "message": "Заявка отправлена",
      "id": "1234567890ABCD",
      "timestamp": 1496411085,
      "data":{
         "sent_date": "2017-06-02",
         "request_number": "127-028"
      }
   },
   {
      "code": 404,
      "message": "Участок не существует",
      "id": "1234567890ABCX",
      "timestamp": 1496411085,
      "data": null
   }
]
```

В приведённом примере для 0-го участка в массиве в качестве дополнительных данных выступают:
- дата отправки заявки в Росрыболовство (*sent_date*);
- номер заявки в Росрыболовство (*request_number*).
