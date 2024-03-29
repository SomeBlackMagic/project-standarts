# Взаимодействия с переменными окружения.

## Базовые принципы 
* По [правилам](https://12factor.net/ru/config) 12 факторной разработки все динамически изменяемые значения должны быть вынесены в переменные окружения
* В коде не должно быть захардкоджено никаких доступов к внешним сервисам/базам данных.
* Из-за большего количества переменных при сборке, переменные который относиться к приложению должны иметь префикс APP_
* Переменные должны быть логически названы для ясности для чего они служат.
* Если переменная не меняется в зависимости от окружения и это не секрет - её нужно вынести в константы кода.

## Работа с переменными локально

В корне репозитория приложение должно иметь закомиченый файл .env в нем описаны все переменные которые потребляет приложение
Для локальной разработки разработчик создает файл `.env.local` в который добавляет только те переменные которые ему нужно переопределить
Файл .env.local находится в `.gitignore`

Приоритеты загрузки переменных в приложение зависят то того как приложение стартует: 

### case-1
Если в момент старта переменные из окружения уже присутствуют в коде - нужно загрузить переменные из `.env` НЕ переопределяя текущие.
Тем самым может произойти дополнение переменных(в случае если каких-то нет в самом окружении)
Далее загружается `.env.local` с переопределением

### case-2
Если переменные в приложение загружаются только кодом тогда приоритет загрузки такой:
 * .env
 * .env.local с переопределением
 * переменные окружения с переопределением 
