
Автоматизация сборки и деплоя Python Docker-приложений через Jenkins + GitHub Webhook

1. Подключение к Jenkins

Перешёл на Jenkins-сервер:
http://158.160.194.244:8080/

Авторизовался под выданными учетными данными.

2. Создание нового Jenkins Pipeline Job

Нажал New Item.

Указал имя проекта в формате student-name-surname.

Выбрал тип Pipeline, нажал OK.

Перешёл в раздел Pipeline → выбрал Pipeline script.

Вставил Jenkinsfile, предоставленный преподавателем.

В Jenkinsfile изменил:

STUDENT_NAME на своё имя.

PORT на уникальный порт 8034.

заменил все hello-student-container → hello-surname-container.

заменил все student-fio-app → student-surname-app.

Сохранил конфигурацию.
<img width="1179" height="206" alt="image" src="https://github.com/user-attachments/assets/bd97341a-c9b8-40b0-a300-01f91cbc893f" />


3. Ознакомление со структурой Jenkinsfile

В Pipeline присутствуют этапы:

Удаление старых контейнеров и образов

Выгрузка кода из GitHub

Сборка Docker-образа

Запуск тестов внутри Docker-контейнера

Запуск контейнера с приложением

Таким образом реализуются основные этапы CI/CD.

4. Настройка GitHub Webhook

Перешёл в свой репозиторий GitHub.

Открыл: Settings → Webhooks → Add webhook.

Указал URL:
http://158.160.194.244:8080/github-webhook/

Content type: application/json.

Триггер: Just the push event.

Сохранил вебхук.
<img width="1123" height="302" alt="image" src="https://github.com/user-attachments/assets/6cdf52df-6cf5-42a9-a970-febb319f6248" />


5. Проверка работы Jenkins

Перешёл в созданную job.

Нажал Build Now.


Проверил запуск приложения в браузере:

http://84.201.147.67:8034/

<img width="1919" height="961" alt="image" src="https://github.com/user-attachments/assets/5a54b861-cee4-450c-ab03-b32027c3a47d" />

Отобразилось приветствие с моим именем.

6. Проверка автоматического запуска через Webhook

Внёс изменения в репозиторий (commit + push).

Убедился, что GitHub отправил событие webhook.

Jenkins автоматически запустил новую сборку.
