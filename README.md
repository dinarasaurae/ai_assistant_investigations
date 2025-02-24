
# README: LLM-ассистент для вопросно-ответной системы

## Описание
Данный Jupyter Notebook реализует обработку пользовательских запросов с использованием модели LLM в рамках вопросно-ответной системы. Скрипт включает этапы уточнения запросов, поиска наиболее релевантных вопросов, ранжирования результатов и генерации ответа на основе найденной информации.

## Функциональность
- **Обработка входного запроса**: принимает пользовательский вопрос и нормализует его.
- **Использование LLM для уточнения**: преобразует исходный запрос в более точный поисковый запрос.
- **Поиск релевантных вопросов**: применяет метод BM25Plus для ранжирования возможных вариантов.
- **Ранжирование кандидатов с помощью LLM**: выбирает наиболее подходящий вопрос из найденных.
- **Генерация ответа**: извлекает ответ на основе готовой базы знаний.
- **Сохранение запроса и ответа**: записывает взаимодействия пользователя в базу данных.

## Требования
- Python 3.10+
- Jupyter Notebook
- Библиотеки: `fastapi`, `aiohttp`, `numpy`, `sqlalchemy`, `asyncpg`, `rank_bm25`, `pydantic_settings`

## Использование
1. Запустите Jupyter Notebook.
2. Выполните ячейки по порядку для загрузки зависимостей и инициализации сервиса.
3. Введите тестовый запрос и выполните обработку.
4. Ознакомьтесь с полученным результатом.

## Входные и выходные данные
- **Вход**: JSON с ключом `question` (например, `{"question": "Как авторизоваться в системе?"}`)
- **Выход**: JSON с уточненным запросом, найденным вопросом и ответом (например, `{"search_query": "Методы авторизации в системе", "matched_question": "Как авторизоваться?", "answer": "Для авторизации используйте..."}`)

## Пример запроса к LLM
```python
request_data = {
    "model": "Qwen/Qwen2.5-32B-Instruct-GPTQ-Int4",
    "messages": [
        {"role": "system", "content": "Преврати пользовательский запрос в точный поисковый запрос."},
        {"role": "user", "content": "Как войти в систему?"}
    ]
}
response = await session.post(LLM_API_URL, json=request_data)
data = await response.json()
print(data)
```

## Разработка и поддержка
Если у вас есть предложения по улучшению или исправлению ошибок, пожалуйста, создайте issue или pull request.

