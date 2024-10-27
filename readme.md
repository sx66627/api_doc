# Archtube api
*Здесь описано взаимодействие с API для получения информации по трансляциям из архива. Формат данных JSON. Использование - backend.*

## URL
*URL для обращения к api*
```
https://api.archtube.space
```

## Методы

### getList
*Получение списка видеозаписей. Используется для вывода на главной.*

Пример:
```
/getList?start={ num }&count={ num }&sort={ old }&key={ key }
```
Параметры:
|Параметр|Тип значения|Описание|
|-|-|-|
|start|число|С какой по счету записи начать вывод (по умолчанию 0)|
|count|число|Количество записей (по умолчанию 10)|
|sort|old|Может принимать значение old, что бы выводить сначала старые записи|
|key (*)|буквы и цифры|Ключ доступа к api|

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|total|число|Общее количество видео (независимо от запроса)|
|videos|массив|Массив видеозаписей|
| | | |
|id|число|id видео|
|title|текст|Название|
|duration|формат времени|Продолжительность видео|
|public_time|число|Время публикации|
|cover|url|Обложка видео|

*Примечание: В ответе total нужен для создания пагинации. Что бы знать максимальное значение для запросов.*

Пример вывода:
```
{
	"total": 281,
	"videos": [
		{
			"id": 2283217998,
			"title": "ЛЕГЕНДА ФОРТНАЙТА O: | !сабка !тг !карта",
			"duration": "02:23:39",
			"public_time": 1729690394,
			"cover": "https:\/\/{ URL скрыт }\/img\/preview\/big\/v2283217998.jpg"
		},
		{
			"id": 2282383365,
			"title": "SILENT HILL 2 ВСЁ ФИНАЛИМ | !сабка !тг",
			"duration": "04:50:41",
			"public_time": 1729600246,
			"cover": "https:\/\/{ URL скрыт }\/img\/preview\/big\/v2282383365.jpg"
		},
		...
	    ]
    }
}
```

### getVideo
*Получение информации о видеозаписи. Используется для воспроизведения видео.*

Пример:
```
/getVideo?id={ num }&key={ key }
```
Параметры:
|Параметр|Тип значения|Описание|
|-|-|-|
|id (*)|число|id видео|
|key (*)|буквы и цифры|Ключ доступа к api|

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|title|текст|Название|
|public_time|число|Время публикации|
|duration|формат времени|Продолжительность видео|
|cover|url|Обложка видео|
|video|url|Ссылка на плейлист для плеера в формате HLS|
|thumbnails|url|Превью для таймлайна (формат WEBVTT)|
|dl|url|Ссылка для скачивания видео в формате mp4|
|video_vip|url|Ссылка на плейлист для плеера в формате HLS **(Для VIP пользователей, например по подписке)**|
|dl_vip|url|Ссылка для скачивания видео в формате mp4 **(Для VIP пользователей, например по подписке)**|

*Примечание: Для VIP отдельные серверы. Не используйте эти URL для всех.*

Пример вывода:
```
[
	{
		"title": "SILENT HILL 2 ВСЁ ФИНАЛИМ | !сабка !тг",
		"public_time": 1729600246,
		"duration": "04:50:41",
		"cover": "https:\/\/{ URL скрыт }\/img\/preview\/big\/v2282383365.jpg",
		"video": "https:\/\/{ URL скрыт }\/hls\/yalexer%20(live)%202024-10-22%2015_30-v2282383365.mp4\/index.m3u8",
		"thumbnails": "https:\/\/{ URL скрыт }\/vtt\/yalexer%20(live)%202024-10-22%2015_30-v2282383365.vtt",
		"dl": "https:\/\/{ URL скрыт }\/dl\/yalexer%20(live)%202024-10-22%2015_30-v2282383365.mp4",
		"video_vip": "https:\/\/{ URL скрыт }\/hls\/yalexer%20(live)%202024-10-22%2015_30-v2282383365.mp4\/index.m3u8",
		"dl_vip": "https:\/\/{ URL скрыт }\/yal\/yalexer%20(live)%202024-10-22%2015_30-v2282383365.mp4"
	}
]
```

### search
*Поиск по видео. Используется для поиска видеозаписей.*

Пример:
```
/search?keywords={ text }&key={ key }
```
Параметры:
|Параметр|Тип значения|Описание|
|-|-|-|
|keywords (*)|текст|Ключевое слово или слова|
|key (*)|буквы и цифры|Ключ доступа к api|

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|total|число|Общее количество найденных видео|
|videos|массив|Массив видеозаписей|
| | | |
|id|число|id видео|
|title|текст|Название|
|duration|формат времени|Продолжительность видео|
|public_time|число|Время публикации|
|cover|url|Обложка видео|

Пример вывода:
```
{
	"total": 3,
	"videos": [
		{
			"id": 1952439460,
			"title": "ранкед diamond 2 | 🎃 обнова скайблоков 1302-8528-0175 | !сабка",
			"duration": "03:31:38",
			"public_time": 1697457407,
			"cover": "https:\/\/{ URL скрыт }\/img\/preview\/big\/v1952439460.jpg"
		},
		{
			"id": 2016914250,
			"title": "общаемся и играем ранкед, чилл стрим перед нг",
			"duration": "03:54:20",
			"public_time": 1703849635,
			"cover": "https:\/\/{ URL скрыт }\/img\/preview\/big\/v2016914250.jpg"
		},
		...
	]
}
```

### getPlayer
*Скрипт плеера. Используется для воспроизведения видео через плеер JWPlayer. (если нужно)*

Пример:
```
/getPlayer?id={ num }&key={ key }
```
Параметры:
|Параметр|Тип значения|Описание|
|-|-|-|
|id (*)|число|id видео|
|key (*)|буквы и цифры|Ключ доступа к api|

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|jwplayer|url|URL для скрипта JWPlayer|
|jw_key|ключ|Скрипт с ключом для JWPlayer|
|script|javascript|Скрипт с заполненными данными для загрузки видео. Для вывода на странице пользователям.|

*Примечание: Обязательно нужно указать ```<div id="jwplayer"></div>``` в месте, где нужно вывести плеер. А так же между тегами ```<head></head>``` вставить url для jwplayer. Не вставляейте статично url для скрипта, т.к. периодически версия будет обновляться и url будет изменен.*

Пример вывода:
```
{
	"jwplayer": "<script src=\"{ URL скрыт }\/jwplayer.js\"><\/script>",
	"jw_key": "<script>jwplayer.key = \"{ jw_key }\";<\/script>",
	"script": "<script>{ script }<\/script>"
}
```

### version
*Получение версии API.*

Пример:
```
/version?key={ key }
```
Параметры:
|Параметр|Тип значения|Описание|
|-|-|-|
|key (*)|буквы и цифры|Ключ доступа к api|

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|version|версия|Версия API|

Пример вывода:
```
{
	"version": "1.0.0 beta"
}
```

## Обработка ошибок
*Если во время запросов возникает ошибка, она будет возвращать соответствующий код и описание.*

Пример (без параметра key):
```
/version
```

Ответ:
|Параметр|Тип значения|Описание|
|-|-|-|
|code|цифры|HTTP код|
|message|текст|Описание ошибки на русском языке|

Пример вывода:
```
{
	"code": 401,
	"message": "Не указан ключ."
}
```

# Дополнительная информация
* Лучшей практикой будет для всех запросов сделать кеширование, хотя бы на 5 минут со стороны клиента (бэкэнд).
* Нигде не показывайте посетителям сайта ключ API, это будет считаться нарушением безопасности и ключ может быть отозван. 
* Значение public_time в формате unixtime во всех методах.
* Все методы возвращают соответствующие коды ошибок, если этот код не 200 (OK).
