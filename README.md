# khadas-vim2 installation Scrypyed

## First step
(https://myoctocat.com/assets/images/base-octocat.svg)
Установите NetworkManager, если его ещё нет:
bash
Copy code
sudo apt update
sudo apt install network-manager
Затем активируйте NetworkManager и выключите другие инструменты для управления сетью (если они есть):
bash
Copy code
sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
Теперь вы можете использовать утилиту nmcli для настройки Wi-Fi:
Просмотреть доступные сети Wi-Fi:
bash
Copy code
<div>
    <button class="copy-button" onclick="copyCodeToClipboard()">Скопировать</button>
</div>


nmcli device wifi list
Подключиться к сети Wi-Fi:
bash
Copy code
nmcli device wifi connect "название_сети" password "пароль"
Замените "название_сети" и "пароль" на соответствующие значения вашей Wi-Fi сети.
После настройки Wi-Fi соединения вы можете добавить его в автозагрузку после перезагрузки системы:
bash
Copy code
nmcli connection modify "название_соединения" connection.autoconnect yes
Замените "название_соединения" на имя вашего соединения.
