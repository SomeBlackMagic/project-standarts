# Взаимодействия с переменными окружения.

## Базовые принципы 
* По [правилам](https://12factor.net/ru/config) 12 факторной разработки все динамически изменяемые значения должны быть вынесены в переменные окружения
* В коде не должно быть захардкоджено никаких доступов к внешним сервисам/базам данных.
* Из-за большего количества переменных при сборке, переменные который относиться к приложению должны иметь префикс APP_

## Работа с переменными локально


В корне репозитория приложение должно иметь закомиченый файл .env в нем описаны все переменные которые потребляет приложение
Для локальной разработки разработчик создает файл `.env.local` в который добавляет только те переменные которые ему нужно переопределить
Файл .env.local находится в `.gitignore`

Приоритеты загрузки переменных в приложение зависят то того как приложение стартует: 

Если в момент старта переменные из окружения уже присутствуют в коде - нужно загрузить переменные из `.env` НЕ переопределяя текущие.
Тем самым может произойти дополнение перемнных(в случае если каких-то нет в в самом окружении)
Далее загружается `.env.local` с переопределением

Если переменные в приложение загружаются только кодом тогда приоритет загрузки такой:
 * .env
 * .env.local с переопределением
 * переменные окружения с переопределением 
