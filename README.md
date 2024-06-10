
![bidon](https://github.com/pnsrc/bidon/assets/28345507/c1f22bdb-e654-4e61-a384-2b423ce21178)
# Bidon

Bidon - это веб-сервер для разработки приложений на платформе 1С-Bitrix. Он включает в себя компоненты, необходимые для запуска и тестирования приложений на 1С-Bitrix, такие как Nginx, PHP-FPM, MySQL, Redis, Adminer, ngrok и Code Server.

## Содержание

- [Установка](#установка)
- [Подключение к базе данных](#подключение-к-базе-данных)
- [Дополнительная информация](#дополнительная-информация)

## Установка

1. Убедитесь, что Docker и Docker Compose установлены на вашем компьютере.
2. Клонируйте репозиторий на ваш компьютер:

    ```bash
    git clone https://github.com/pnsrc/bidon.git
    cd bidon
    ```

3. Укажите необходимые настройки в файле `docker-compose.yaml`:

    - `NGROK_AUTHTOKEN`: Замените на ваш токен аутентификации ngrok. Получите токен на [официальном сайте ngrok](https://dashboard.ngrok.com/get-started/your-authtoken).
    - `PASSWORD`: Замените на ваш пароль для Code Server.

4. Запустите приложение с помощью Docker Compose:

    ```bash
    docker-compose up -d
    ```

5. Все сервисы будут доступны по следующим адресам:

    - **Nginx (web)**: http://localhost:80
    - **Adminer**: http://localhost:8081
    - **Code Server**: http://localhost:8082
    - **ngrok**: Публичный URL будет отображен после запуска контейнера ngrok.

6. Чтобы установить 1С-Bitrix, перейдите по адресу:

    ```plaintext
    http://localhost/bitrixsetup.php
    ```

## Подключение к базе данных

При настройке 1С-Bitrix используйте следующие параметры для подключения к базе данных:

- **Хост**: `db` (имя сервиса базы данных в docker-compose.yaml)
- **Пользователь**: `bitrix`
- **Пароль**: `root_password`
- **Имя базы данных**: `bitrix`

Вы также можете использовать Adminer для управления базой данных через веб-интерфейс:

1. Перейдите по адресу [http://localhost:8081](http://localhost:8081).
2. Введите следующие параметры для подключения:
   - **Сервер**: `db`
   - **Пользователь**: `bitrix`
   - **Пароль**: `root_password`
   - **База данных**: `bitrix`

## Дополнительная информация

Если отсутствует доступ к записи, откройте контейнер `bidon-php` и выполните следующие команды:

```bash
docker exec -it bidon-php sh
cd /
chmod -R 777 /var/www/html/
```

[Code Server](https://github.com/cdr/code-server) - это удаленная версия Visual Studio Code, работающая в локальной среде. Он предоставляет полный функционал VS Code через веб-браузер. Code Server запускается и доступен по адресу [http://localhost:8082](http://localhost:8082).

> **Важно**: Code Server не будет доступен через ngrok, так как ngrok настроен только для перенаправления HTTP-запросов на порт 80, который используется веб-сервером Nginx.
