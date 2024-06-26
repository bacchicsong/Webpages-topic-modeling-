# Тематическое моделирование веб-страниц российского сегмента интернета
***Статус: завершён***

Цель заключается в определении тематик примерно 6 000 000 сайтов доментов .ru, .su, .рф.

Пайплайн кратко: собрать и обработать текстовую информацию с ~6 000 000 сайтов, создать эмбеддинги данных для каждого сайта, провести кластеризацию над эмбеддингами.

В папках с этапами проекта содержатся относящиеся к ним файлы и их описание. Ниже находится описание самих этапов.

### Этап 1. Сбор данных
***Статус: завершён***

Вначале были найдены все сайты доменов .ru, .su, .рф, источником которых послужил ресурс [https://statonline.ru/].

С веб-страниц, на которые ведут имеющиеся ссылки, необходимо собрать данные, по которым можно понять их тематику. Решено собирать: метаданные (описание, заголовки, ключевые слова) и всю текстовую информацию. 

Парсинг данных осуществляется инструментами библиотек requests, BeautifulSoup и запараллелен с помощью библиотеки multiprocessing, так как иначе он проходит очень медленно.

### Этап 2. Обработка данных, создание эмбеддингов 
***Статус: завершён***

Собранная текстовая информацию и метаданные каждого сайта объединяются в одну строку, после чего удаляются сайты, о которых информацию не получить (либо отсутствуют данные из-за особенностей HTML-кода, либо произошла ошибка при скрапинге). Далее проводится удаление стоп слов, лемматизация строки.

Эмбеддинги обработанных слов создаются с помощью модели fasttext [https://huggingface.co/facebook/fasttext-ru-vectors] (другие модели, например, [https://huggingface.co/cointegrated/rubert-tiny2] слишком долго обрабатывают данные).

Планируется, что данные будут объёмные, что не позволит их полностью хранить в ОЗУ. Предусматривается построчная обработка файлов с диска.

### Этап 3. Кластеризация 
***Статус: завершён***

Над эмбеддингами с помощью KMeans совершается кластеризация на 100 кластеров. Далее каждой строке текстовой информации сопоставляется номер её кластера и строится облако слов. После этого удаляются неинтерпретируемые кластеры и заново производится деление уже на 50 кластеров.






