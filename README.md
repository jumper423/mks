# “МКС” - “многофункциональный кабинет соцработника” 

“МКС” - это CRM-система для организации сопровождения клиентов и учета оказанных услуг, а также для сбора статистики. Ей могут пользоваться соцработники, юристы и другие сотрудники как НКО, так и государственных учреждений соцобслуживания. 

В первую очередь, “МКС” подойдет организациям, помогающим бездомным людям - в этом случае она нуждается в минимальной настройке для нужд конкретной организации. Другие организации (например, помогающие наркопотребителям или ЛЖВ) также смогут пользоваться “МКС”, изменив список предоставляемых услуг и настроив другие разделы. Большую часть настроек можно осуществить силами простых сотрудников, без привлечения it-специалиста. 

Центральным звеном системы является профиль клиента. Страница профиля  содержит анкету, информацию обо всех оказанных услугах, примечания сотрудников, автоматическую генерацию справок и других документов. К профилю можно прикрепить файлы в любых форматах, настроить напоминания, внести данные о проживании в приюте, если таковой у вас имеется. В разделе “Сервисный план” можно составить долгосрочный план сопровождения и отмечать начало и окончание работы по конкретным задачам.

У каждого сотрудника есть личный кабинет, в котором ведется учет всей рабочей активности. Удобная система поисковых фильтров позволяет найти любую информацию, когда-либо внесенную в базу.

Раздел “Отчеты” позволяет отслеживать все выполненные работы по предоставлению разовых услуг и сопровождению - как по организации в целом, так и по конкретным работникам..

Подробнее об “МКС” можно узнать, посмотрев скринкаст - https://youtu.be/f07ObZ91q8k

Если вы хотите установить “МКС”, у нас к вам две просьбы: во-первых, разворачивая систему на вашем сервере, пожалуйста, не забудьте позаботиться о защите персональных данных ваших клиентов и сотрудников. Во-вторых, заполните, пожалуйста, небольшую [анкету](https://goo.gl/forms/YjhAaqSaxAvxMKoE3), чтобы мы знали, для кого трудились :)

Будем рады обратной связи. И добро пожаловать на борт!


## Шаги установки

1. Склонируйте репозиторий проекта:

    > git clone  https://github.com/homelessru/mks.git

2. После клонирования перейдите в каталог проекта:

    > cd homeless

3. Создайте локальные копии файлов `docker-compose.yml.dist` и `.env.dist`:
    
    > cp docker-compose.yml.dist docker-compose.yml
    
    > cp .env.dist .env
    
    > cp shared/homeless/app/config/parameters.yml.dist shared/homeless/app/config/parameters.yml

    При необходимости укажите нужные настройки в этих файлах.

4. Запустите сборку контейнеров:
    Если докен не установлен, то сначала
    
    ``` 
    curl -fsSL get.docker.com -o get-docker.sh
    sh get-docker.sh
    ```
    
    после собираем конейнеры

    > docker-compose build
    

5. После успешного окончания сборки, запустите ее:

    > docker-compose up -d

6. Подсоединитесь к symfony-приложению, запустив:
    
    > ./docker/docker/docker-symfony

7. С помощью `composer` установите необходимые библиотеки, затем укажите параметры подключения к БД:

    > composer install

8. Запустите миграцию для создания первоначальной структуры базы данных и заполнения данными: 

    > ./app/console doctrine:migrations:migrate

9. При желании можете поменять пароль для входа в систему

    > ./app/console fos:user:change-password admin

10. Сгенерируйте необходимые assets:

    > ./app/console fos:js-routing:dump

    > ./app/console assetic:dump --symlink

11. Настройте хост для проекта, перейдите по адресу хоста, 
если пароль не был изменен на шаге 9 - залогиньтесь с доступом `admin/password`.
