# Отчёт по дополнительному заданию по курсу ABC-Unix
## Протокол  работы:
### Установка и включение docker-machine.

*С помощью git bash устанавливаем докер машину.*

    if [[ ! -d "$HOME/bin" ]]; then mkdir -p "$HOME/bin"; fi && \   --Если в домашнем каталоге нет папки bin создаём её
    curl -L https://github.com/docker/machine/releases/download/v0.10.0/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" && \ --скачиваем файл с указанием в какую папку скачать и как назвать
    chmod +x "$HOME/bin/docker-machine.exe"  --даём права на запуск
  
![1](/images/1.png)

по [ссылке](https://get.docker.com/builds/Windows/x86_64/docker-17.04.0-ce.zip) или выбрав [версию](https://github.com/docker/docker/releases) скачиваем клиент docker, кладём файл docker.exe в папку с docker-machine и выполняем команду

>chmod +x "$HOME/bin/docker.exe"

### или просто устанавливаем DockerToolbox

*также для того чтобы запускать докер из Windows cmd необходимо выполнить команду:*

>setx path "%path%;C:\Users\\[User]\bin" /M

*командой create создаём новую машину.*

>docker-machine create [имя машины]
  
![2](/images/2.png)

*командой ls проверяем создание новой машины и её статус*

>docker-machine ls

![3](/images/3.png)

команда start запускает машину
>docker-machine start [name] 

команда stop запускает машину
>docker-machine stop [name] 

## Вариант 1

*командой ssh подключаемся к ней*

>docker-machine ssh [имя машины]

![4](/images/4.png)

## Вариант 2

командой eval активируем окружение машины

>eval $("C:\Users\[User]\bin\docker-machine.exe" env new)

(команда копируется из docker-machine env [name] последняя строка)

![15](/images/15.png)

*и дальше просто используем команды docker*

### Создание контейнера

*командой docker run создаём контейнер из репозитория и запускаем его*

>docker run -d -t --privileged -h lxc21 --name lab01 vlavad/lab00

*командой docker ps проверяем установку и статус*

>docker ps -a

*командой docker exec входим в контейнер*

>docker exec -i -t lab<NN> /bin/bash

![5](/images/5.png)

данная команда работает в cmd, но в git bash (при использовании машины без подключения по ssh) нужно модифицировать команду:

>winpty docker exec -it l1 bash

![16](/images/16.png)

*для остановки контейнера используеся команда poweroff от пользователя root*

*для запуска контейнера используется команда docker start [имя контейнера]*

### Выполнение лабораторных работ в контейнере

*командой ls проверяем содержимое корневого каталога*
*командой cd /run/systemd && ls переходим в каталог systemd и выводим содержимое*

>ls
>cd /run/systemd && ls

![6](/images/6.png)

*командой journalctl просмотрим системный журнал*

>journalctl

![7](/images/7.png)

*командой timedatectl проверим настройку времени, даты и временной зоны*

>timedatectl status

![8](/images/8.png)

*командой systemctl list-unit-files выполняется просмотр сервисов*

>systemctl list-unit-files

![9](/images/9.png)

нет работающего сервиса network 

![10](/images/10.png)

*командой ifconfig выведем параметры сетевых интерфейсов*

>ifconfig

![11](/images/11.png)

*командой route выведем статические маршруты сети*

>route

![12](/images/12.png)

### Создание протокола работы

Для создания протокола работы требуется перенаправить выходной поток команды в файл с помощью >>

Пример:

>route >> file

При необходимости файл можно отредактировать с помощью редактора

> nano file

*Для того чтобы протокол выводился при входе в систему необходимо добавить скрипт в каталог /etc/profile.d*

>cd /etc/profile.d

>touch my.sh

>chmod 777 my.sh

![13](/images/13.png)

### Создание образа и загрузка в репозиторий

*командой login подключаемся к своему репозиторию*

>docker login
>username
>password

*командой commit создаём образ контейнера*

>docker commit [cont_name] [your_rep]

*командой push загружаем образ в репозиторий*

>docker push [your_rep]

![14](/images/14.png)

### Вывод

[репозиторий работы](https://hub.docker.com/r/alxloginov/lab01/)

В данной работе был установлена docker-machine на базе ОС Windows. Были изучены методы работы с машиной, dockerом и репозиторием docker hub. Также были изучены отличительные особенности систем с systemd.

