# Установка Scrypted

## Настройки Wi-Fi 
После перезагрузки системы автоматически подключатся к Wifi в таком случае, вам, возможно, потребуется использовать другие инструменты для настройки сети. Один из распространенных способов - использование NetworkManager. Вы можете установить и настроить Wi-Fi соединение с помощью NetworkManager следующим образом:

Расскажите как установить и использовать ваш проект, покажите пример кода:

1. Установите NetworkManager, если его ещё нет:
```sh
sudo apt update
sudo apt install network-manager
```

2. Затем активируйте NetworkManager и выключите другие инструменты для управления сетью (если они есть):
```typescript
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
```

3.Теперь вы можете использовать утилиту nmcli для настройки Wi-Fi:
- Просмотреть доступные сети Wi-Fi:
```typescript
nmcli device wifi list
```
- Подключиться к сети Wi-Fi:
```typescript
nmcli device wifi connect "название_сети" password "пароль"
```
Замените "название_сети" и "пароль" на соответствующие значения вашей Wi-Fi сети.

4. После настройки Wi-Fi соединения вы можете добавить его в автозагрузку после перезагрузки системы:
```typescript
nmcli connection modify "название_соединения" connection.autoconnect yes
```
Замените "название_соединения" на имя вашего соединения.

## Установка Docker на Khadas VIM2
Установка Docker на устройство Khadas VIM2 под управлением Ubuntu может быть выполнена следующим образом:

#### 1. Обновление пакетов:
В начале рекомендуется обновить список пакетов и установить все доступные обновления. Выполните следующие команды в терминале:
```sh
sudo apt update
sudo apt upgrade
```


#### 2. Установка зависимостей:
Для установки Docker вам потребуется некоторые зависимости. Выполните следующую команду, чтобы убедиться, что все необходимые зависимости установлены:
```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

#### 3.Добавление репозитория Docker:
Добавьте официальный GPG-ключ Docker и добавьте репозиторий Docker к вашей системе:
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#### 4. Установка Docker:
Теперь установите Docker, выполнив следующие команды:
```sh
sudo apt update
sudo apt install docker-ce
```

#### 5. Запуск и добавление в автозагрузку:
После успешной установки Docker можно запустить службу Docker и добавить ее в автозагрузку:
```sh
sudo systemctl start docker
sudo systemctl enable docker
```

#### 6.Проверка установки:
Выполните команду docker --version, чтобы убедиться, что Docker установлен корректно:
```sh
docker --version
```
Теперь у вас должен быть установлен Docker на вашем устройстве Khadas VIM2 под управлением Ubuntu. Вы можете начать использовать Docker для запуска и управления контейнерами.


## Установка Scrypted
1. Репозиторий для Ubuntu/Debian
Пользователи рабочего стола на Ubuntu должны устанавливать приложение с использованием apt, чтобы автоматически получать обновления.
```sh
echo 'deb [trusted=yes] https://nuts.scrypted.app/apt stable main' | sudo tee /etc/apt/sources.list.d/scrypted.list
sudo apt update
sudo apt install scrypted-electron
```

2. Создать нового пользователя.
```sh
adduser имя
```
```sh
usermod -aG sudo имя
```

3. Этот скрипт загрузит все зависимости, включая Docker (его можно пропустить, см. ниже), а также файл docker-compose.yml и установит Scrypted как службу.

Используйте кнопку "Копировать" в фрагменте ниже, чтобы скопировать весь скрипт, а затем вставьте содержимое в Терминал, чтобы установить Scrypted.
```sh
mkdir -p ~/.scrypted
curl -s https://raw.githubusercontent.com/koush/scrypted/main/install/docker/install-scrypted-docker-compose.sh > ~/.scrypted/install-scrypted-docker-compose.sh 
sudo SERVICE_USER=$USER bash ~/.scrypted/install-scrypted-docker-compose.sh
```
- При установке будет предложено установить Docker и настроить внешнее хранилище для Scrypted NVR. Установка Docker обязательна, поэтому это предоставляет способ пропустить автоматическую установку. Внешнее хранилище полностью необязательно и может быть настроено позже.

Scrypted теперь работает по адресу: https://localhost:10443/

Обратите внимание, что это `https` и вас попросят подтвердить или игнорировать сертификат веб-сайта.

## docker-compose.yml location

The [docker-compose.yml](https://github.com/koush/scrypted/blob/main/install/docker/docker-compose.yml) is stored at `~/.scrypted/docker-compose.yml`.
