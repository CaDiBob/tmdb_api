
# Поиск фильмов на сайте [TMDB](https://www.themoviedb.org/).

### Получение ключа к API.

Для работы скриптов нужно получить ключа к API сайта [TMDB](https://www.themoviedb.org/), пройти процедуру [регистрации](https://www.themoviedb.org/signup),
подтвердить адрес эл.почты авторизоваться и [создать ключ к API в настройках вашей учетной записи.](https://www.themoviedb.org/settings/api)

### Скрипт `make_own_db.py`.

Запрашивает ключ к [API](https://www.themoviedb.org/) TMDB, если API введен не корректно выдаст ошибку `Invalid api key` и завершит работу скрипта, если корректен создает базу данных.
Пример корректного запроса к API и создание БД:
```
please, wait, this operation may take smth like 15-20 minutes
0.0 percent complete
0.1 percent complete
0.2 percent complete
0.3 percent complete
0.4 percent complete
0.5 percent complete
0.6 percent complete
0.7 percent complete
0.8 percent complete
0.9 percent complete
.....
99.8 percent complete
99.9 percent complete
```
По окончанию работы будет создана БД с названием `MyFilmDB.json` на 1000 фильмов с [сайта TMDB](https://www.themoviedb.org/), в корневой папке скрипта.

### Скрипт `own_db_helpers.py`.
Проверяет наличие БД, если таковая есть реализует ее чтение, если нет корректно завершит работу.

### Скрипт `search_in_db.py`.
Ищет в созданной БД `MyFilmDB.json` в соответствии с названием, фильм или коллекцию фильмов относящихся к друг другу франшизa, трилогия, и т.п. например при вводе названия `The Lord of the Rings`
вывод программы будет такой:
```
The Lord of the Rings: The Fellowship of the Ring
The Lord of the Rings: The Return of the King
The Lord of the Rings: The Two Towers
```
Если фильм отсутствует в базе корректно завершит работу.

### Скрипт `find_similar.py`:
На основе введённого вами названия фильма выдает список рекомендаций к просмотру.
Например, при вводе названия фильма `The Devil Wears Prada` вывод будет примерно такой:

```
Bend It Like Beckham
Chocolat
Forrest Gump
Garden State
Harold and Maude
Lost in Translation
Manhattan
Muriel's Wedding
The Apartment

```
### Скрипт `hello_api_TMDB.py`.
Возвращает бюджет фильма, `id` которого вы укажите в скрипте в это поле: `movie_number = 176`
Код скрипта:
```Python
from tmdb_helpers import get_user_api_key
from tmdb_helpers import make_tmdb_api_request

if __name__ == '__main__':
    user_api_key = get_user_api_key()
    if not user_api_key:
        print('Invalid api key')
        raise SystemExit
    movie_number = 176
    print(make_tmdb_api_request(method='/movie/%d' % movie_number, api_key=user_api_key)['budget'])
```
При запуске скрипт просит вас ввести ключ к [API TMDB](https://www.themoviedb.org/), если ключ не корректный выдаст ошибку и завершит работу скрипта.
Пример некорректного ввода API:
```
Enter your api key v3:
Invalid api key
```
Пример корректного ввода API:
Вывод в консоль будет такой:
```
Enter your api key v3:
1200000

```

### Скрипт `tmdb_helpers.py`.
Делает запрос к API TMDB, выдаст исключение и корректно завершит работу скрипта, если был введен не верный ключ к API или отсутствует соединения с интернетом.

### Запуск.

Запуск всех скриптов производить из командной строки.
Пример:
```
user@home:~/Рабочий стол$ python hello_api_TMDB.py

```

### Установка зависимостей.

Python3 должен быть уже установлен. 
Затем используйте `pip` (или `pip3`, есть конфликт с Python2) для установки зависимостей:
```
pip install -r requirements.txt
