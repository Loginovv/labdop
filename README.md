# Отчёт по дополнительному заданию по курсу ABC-Unix
## Протокол  работы:
### Установка и включение docker-machine.

*С помощью git bash устанавливаем докер машину.*

>if [[ ! -d "$HOME/bin" ]]; then mkdir -p "$HOME/bin"; fi && \
>curl -L https://github.com/docker/machine/releases/download/v0.10.0/docker-machine-Windows-x86_64.exe > "$HOME/bin/docker-machine.exe" && \
>chmod +x "$HOME/bin/docker-machine.exe"
  
![1](/images/1.png)

*командой create создаём новубю машину.*

>docker-machine create [имя машины]
  
![2](/images/2.png)

*командой ls проверяем создание новой машины и её статус*

>docker-machine ls

![3](/images/3.png)

*командой ssh подключаемся к ней*

>docker-machine ssh [имя машины]

![4](/images/4.png)

### Создание контейнера

*командой docker run создаём контейнер из репозитория и запускаем его*

>docker run -d -t --privileged -h lxc21 --name lab01 vlavad/lab00

*командой docker ps проверяем установку и статус*

>docker ps -a

*командой docker exec входим в контейнер*

>docker exec -i -t lab<NN> /bin/bash

![5](/images/5.png)

*для остановки контейнера используеся команда poweroff от пользователя root*

*для запуска контейнера используется команда docker start [имя контейнера]*

![6](/images/6.png)
![7](/images/7.png)
