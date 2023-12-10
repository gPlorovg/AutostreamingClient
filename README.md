# AutostreamingOBS

Проект является частью более крупного проекта по удалённому управлению режесёрского пульта с использованием свободного програмного обеспечения OBS studio

## Предустановки
1. OBS Studio v29.1.3 и выше
2. Python v3.11 и выше

## Регламент установки клиентского приложения Autostreaming

1. Склонировать репозиторий AutostreamingClient
2. Открыть powershell и перейти в папку с проектом
3. Установить все зависимости (для глобального Python интерпретатора)
```
pip install -r requirements.txt
```
4. Запустить файл "launch.py"
```
python .\launch.py
```
5. Ввести необходимые данные
```
Input MQTT username:
Input MQTT password:
```
6. Сохранить данные
```
Autorun command for Autostreaming client app:
DATA1
Python Path:
DATA2
```
7. Запустить от имени Администратора powershell
8. Ввести полученнию команду (DATA1)
```
УСПЕХ. Запланированная задача "Autostreaming" была успешно создана.
```
9. Запустить клиентское приложение
```
pythonw.exe .\client.py
```
10. В открывшемся окне OBS studio настроить Python интерпретатор - указать (DATA2)
```
Сервис -> Скрипты -> Настройки Python
```
11. В папке проекта появился файл "obs_script.py", его  необходимо загрузить в OBS studio
```
Сервис -> Скрипты -> +
``` 

12. В журнале скрипта должена появиться строка говорящая об успешном подключении
```
Connected with result code 0
```

### Клиентское приложение

Скрипт client.py запускается в фоновом режиме с помощью pythonw.exe
Клиентское приложение поддерживает Obs studio во включённом состоянии и постоянно отправляет статус Obs studio на сервер, используя протокол MQTT

### OBS скрипт

Скрипт obs_script.py используется внутри Obs студио
Он ведет пингование ip источников медиа, которые в свою очередь являются потоками данных с ip камер, и отправляет данные на сервер по протоколу MQTT

### Серверный скрипт

Скрипт server.py запускается на сервере и собирает информацию, пришедшею как с клиентских приложений, так и со скриптов Obs, а также отправляет запрос на пингование
