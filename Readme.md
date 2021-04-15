1. git clone https://github.com/Raikh/rtest-docker.git
2. Отредактировать конфиг nginx (./conf.d/rtest.conf), указав нужный server_name
3. Отредактировать конфиг приложения (./env/env.backend). APP_URL 
4. Сборка и запуск окружения `docker-compose up -d`. При первом запуске MySQL проинициализируетсяи создаст нужную БД и пользователя, после чего контейнер перезапускается.
5. Выполнить миграции и сиды `docker-compose exec backend php artisan migrate --seed`
6. Обработка запланированных переводов осуществляется по расписанию, так что необходимо в крон добавить `* * * * * /usr/bin/env docker-compose -f /path/to/project/docker-compose.yml exec -T backend php artisan schedule:run >> /dev/null 2>&1`
7. По-умолчанию будет отвечать по http://localhost
