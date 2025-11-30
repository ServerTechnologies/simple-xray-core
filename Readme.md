# Скрипт для лёгкой установки и настройки ядра X-ray без графического интерфейса

Вы все знакомы с такими панелями управления, как 3x-ui, Marzban и другими. Все эти панели являются всего лишь графическими надстройками над ядром X-ray и служат для удобного управления им, а также для создания подключений и настроек. Ядро же может работать без всяких панелей и управляться полностью через терминал. Основное преимущество использования «голого» ядра заключается в том, что вам не нужно заморачиваться с доменами и TLS-сертификатами. Само ядро можно установить и администрировать вручную с помощью официальной документации. Этот скрипт предназначен для упрощения этой задачи: он автоматически установит ядро на сервер, создаст конфигурационные файлы и несколько исполняемых файлов для удобного управления пользователями.

## VPS для панели

Для установки панели нам понадобится VPS-сервер. Приобрести его можно в [ishosting](https://bit.ly/3rOqvPE).  
В сервисе доступны более 36 локаций. Если вам не нужна какая-то конкретная страна, выбирайте ту, что ближе к вам.

## Системные требования

- 1 CPU  
- 1 GB RAM  
- 10 GB диска  
- ОС Ubuntu 22 x64 или Ubuntu 24 x64


## Как пользоваться скриптом. Старая инструкция из видео. Установка с протоколом Vless TCP Reality

Скрипт создавался и тестировался под ОС Ubuntu 22 x64 и Ubuntu 24 x64. На других ОС может работать некорректно. Чтобы скачать и запустить скрипт, используйте эту команду:

```sh
wget -qO- https://raw.githubusercontent.com/ServerTechnologies/simple-xray-core/refs/heads/main/xray-install | bash
```

## Команды для управления пользователями

**Вывести список всех клиентов:**

```sh
userlist
```

**Вывести ссылку и QR-код для подключения основного пользователя:**

```sh
mainuser
```

**Создать нового пользователя:**

```sh
newuser
```

**Удалить пользователя:**

```sh
rmuser
```

**Создать ссылку для подключения:**

```sh
sharelink
```

В домашней папке пользователя будет создан файл `help` — в нём содержатся подсказки с описанием команд. Посмотреть его можно с помощью команды (нужно находиться в домашней папке пользователя):

```sh
cat help
```

## Проблемы с доступом по протоколу Vless на транспорте TCP.
> Многие заметили, что с доступностью Vless на транспорте TCP наблюдались некоторые проблемы. Я добавил вариацию этого скрипта с протоколом XHTTP. Важно! XHTTP - сравнительно новый транспорт, поэтому далеко не все клиенты его поддерживают. Список клиентов есть в текстовой версии видео на Github.
- [Ссылка на видео YouTube про XHTTP](https://youtu.be/XASBkzQE00s)
- [Текстовая версия видео на Github](https://github.com/ServerTechnologies/3x-ui-with-xhttp)

Если вы уже установили ядро по видео с транспортом tcp, не спешите все сносить и устанавливать XHTTP. Для начала просто обновите ядро командой
```sh
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```
Если обновление не помогло, то можно приступать к установке новой версии скрипта с транспортом XHTTP. На всякий случай создадим бэкап файла конфигурации и файла с ключами, если вдруг захочется откатится обратно на tcp
```sh
cp /usr/local/etc/xray/config.json /usr/local/etc/xray/config.json.old
cp /usr/local/etc/xray/.keys /usr/local/etc/xray/.keys.old
```
Чтобы восстановить конфигурацию, введите:
```sh
wget -qO- https://raw.githubusercontent.com/ServerTechnologies/simple-xray-core/refs/heads/main/xray-install | bash
mv /usr/local/etc/xray/config.json.old /usr/local/etc/xray/config.json
mv /usr/local/etc/xray/.keys.old /usr/local/etc/xray/.keys
systemctl restart xray
```
Будет переустановлено ядро, восстановлена старая конфигурация, в том числе старые клиенты.

## Установка с транспортом XHTTP.
Установка производится слудующей командой
```sh
wget -qO- https://raw.githubusercontent.com/ServerTechnologies/simple-xray-core/refs/heads/main/xhttp-xray-install | bash
```
Команды для управления пользователями те же самые, что и в предыдущем пункте


## Полезные ссылки

- [GitHub проекта X-ray Core](https://github.com/XTLS/Xray-core)
- [Официальная документация на русском](https://xtls.github.io/ru/)

## Клиенты для подключения

**Windows**

- [v2rayN](https://github.com/2dust/v2rayN)  
- [Furious](https://github.com/LorenEteval/Furious)  
- [Invisible Man - Xray](https://github.com/InvisibleManVPN/InvisibleMan-XRayClient)  

**Android**

- [v2rayNG](https://github.com/2dust/v2rayNG)  
- [X-flutter](https://github.com/XTLS/X-flutter)  
- [SaeedDev94/Xray](https://github.com/SaeedDev94/Xray)  

**iOS & macOS arm64**

- [Streisand](https://apps.apple.com/app/streisand/id6450534064)  
- [Happ](https://apps.apple.com/app/happ-proxy-utility/id6504287215)  
- [OneXray](https://github.com/OneXray/OneXray)  

**macOS arm64 & x64**

- [V2rayU](https://github.com/yanue/V2rayU)  
- [V2RayXS](https://github.com/tzmax/V2RayXS)  
- [Furious](https://github.com/LorenEteval/Furious)  
- [OneXray](https://github.com/OneXray/OneXray)  

**Linux**

- [Nekoray](https://github.com/MatsuriDayo/nekoray)  
- [v2rayA](https://github.com/v2rayA/v2rayA)  
- [Furious](https://github.com/LorenEteval/Furious)  

## Если вдруг нужно удалить, то воспользуйтесь этими командами:
```sh
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ remove
rm /usr/local/etc/xray/config.json
rm /usr/local/etc/xray/.keys
rm /usr/local/bin/userlist
rm /usr/local/bin/mainuser
rm /usr/local/bin/newuser
rm /usr/local/bin/rmuser
rm /usr/local/bin/sharelink
```
