---
title: "Как подключиться к удаленному узлу в GUI кошельке"
categories:
  - "Руководства"
comments: false
authorbox: false
pager: true
toc: true
mathjax: true
sidebar: "right"
---

## _Убедитесь в том, что ваш кошелёк работает в Advanced mode (Продвинутый режим)_

Чтобы использовать специализированный удалённый узел, ваш кошелек должен находиться в Advanced mode (Продвинутый режим). Simple mode (Простой режим) и Bootstrap (Простой режим с использованием узла начальной загрузки) не поддерживают эту возможность.

Чтобы проверить, работает ли ваш кошелёк в продвинутом режиме, зайдите в `Settings` (Настройки) > `Info` (Информация) и проверьте `Wallet mode` (Режим кошелька).

Если ваш кошелёк не находится в Advanced mode (Продвинутый режим), вам нужно будет изменить его (см. следующий шаг).

Если ваш кошелёк уже работает в Advanced mode (Продвинутый режим), вы можете пропустить следующий шаг.

![01](/img/manuals/how-to-connect-gui-to-remote-node/01.png)

### _Переключение вашего кошелька в Advanced mode (Продвинутый режим)_

Если ваш кошелёк открыт, вам нужно сначала закрыть его. Чтобы сделать это, перейдите в `Settings` (Настройки) > `Wallet` (Кошёлек) > `Close this wallet` (Закрыть текущий кошелек)

![02](/img/manuals/how-to-connect-gui-to-remote-node/02.png)

Откроется главное меню: экран `Welcome to Monero` (Добро пожаловать в Monero). В левом нижнем углу нажмите кнопку `Change wallet mode` (Изменить режим кошелька), а на следующей странице выберите `Advanced mode` (Расширенный режим). Затем снова откройте файл кошелька.

![03](/img/manuals/how-to-connect-gui-to-remote-node/03.png)

![04](/img/manuals/how-to-connect-gui-to-remote-node/04.png)

## _Поиск публичного удаленного узла_

Сначала нужно найти публичный удалённый узел, к которому можно подключиться. На веб-сайте [moneroworld.com](https://moneroworld.com/#nodes) размещена подробная информация, касающаяся того, как находить публичные узлы. Одним из самых простых способов является использование удалённого узла, поддерживаемого сервисом moneroworld, но у них также есть инструмент для поиска случайных узлов.

## _Настройка вашего кошелька перед подключением к пубчичному удаленному узлу_

При открытии вашего кошелька появится всплывающее окно с опцией `Use custom settings` (Использовать собственные настройки). Нажмите на него, и вы будете перенаправлены на страницу `Settings` (Настройки) > `Node` (Узел).

Если вы не видите этого всплывающего окна, то перейдите на страницу `Settings` (Настройки) > `Node` (Узел).

![05](/img/manuals/how-to-connect-gui-to-remote-node/05.png)

На этой странице выберите `Remote Node` (Удаленный узел).

В поле `Address` (Адрес) следует ввести адрес удалённого узла, к которому вы хотите подключиться. Этот адрес может выглядеть, как `node.moneroworld.com`, или же, как любой IP-адрес.

В поле `Port` (Порт) следует указать номер порта удалённого узла. Если удалённый узел будет указан, как `node.moneroworld.com:18089`, адресом будет `node.moneroworld.com`, а номером порта -`18089`. По умолчанию номер порта указывается, как `18081`, но он может варьироваться в зависимости от узла, к которому вы пытаетесь подключиться.

Если ваш удаленный узел требует аутентификации, вы можете ввести имя пользователя в поле `Daemon username` (Имя пользователя демона) и пароль в `Daemon password` (Пароль демона).

Наконец, нажмите кнопку `Connect` (Подключиться) и дождитесь, пока ваш кошелёк не подсоединится к удалённому узлу.