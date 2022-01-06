---
title: "Релиз 8-ой бета-версии кошелька Feather"
date: "2021-07-12"
categories:
  - "Новости"
tags:
  - "Feather Wallet"
lead: "Состоялось обновление Feather Wallet до 8-ой бета-версии."
pager: true
toc: false
sidebar: "right"
widgets:
  - "recent"
  - "taglist"
---

_Файлы для скачивания_: https://featherwallet.org/download/  

_Хеши_: https://featherwallet.org/files/releases/hashes-beta-8.txt  

### _Журнал изменений_:  

![](/img/post/2021-07-12-feather-beta8-released-trezor-webcam-qr/01.jpg)

_**Новые возможности и улучшения**_:
- Реализация поддержки аппаратного кошелька Trezor.
- Добавления сканера QR-кодов через веб-камеру.
- Примечание: сканер в настоящее время не поддерживается отдельными двоичными файлами Linux. Если вы работаете с Linux, и хотите воспользоваться новой возможностью, скачайте образ приложения.
- Теперь можно скопировать изображение QR-кода непосредственно в воле Pay To (Оплатить), после чего адрес будет заполнен автоматически (а также описание и сумма. Если это запрос платежа).
- Диалоговое окно QR-кода: QR-код теперь масштабируется вместе с размером диалогового окна.
- Возможность одновременного перевода множества входов: теперь в закладке Coins (Монеты) можно выбрать сразу множество монет и перевести их в одной транзакции.
- Монеты теперь можно помечать.
- Примечание: в данный момент ярлыки привязываются к описанию транзакции. Сообщите, если способ вашего использования требует более точного контроля.
- В закладку Coins добавлена панель поиска.
- Неподтверждённые транзакции теперь сохраняются в кеше кошелька и могут ретранслироваться после того, как кошелёк будет открыт снова. До этого обновления ретрансляция была возможна только в том случае. Если кошелёк оставался открытым после отправки транзакции.
- Во время начальной настройки обнаруживается наличие локального узла на порте, установленном по умолчанию. Feather автоматически предлагает подсоединиться к нему, а не к стороннему узлу.
- Добавлен инструмент, позволяющий проверить: 1) является ли адрес действительным, 2) принадлежит ли он открытому в настоящий момент кошельку, 3) какому подадресу он принадлежит. Инструмент можно найти, выбрав Tools → Address Checker.
- Список майнинг-пулов в закладке Mining (Майнинг) теперь можно конфигурировать.
- Встроенный Tor обновлён до версии v0.4.6.6 (Windows/Linux).
- Сборки Linux теперь являются постоянно воспроизводимыми.
- В диалоговое окно, появляющееся сразу после отправки транзакции, добавлена кнопка, позволяющая посмотреть подробную информацию транзакции.
- Теперь для отображения мнемонической фразы и диалогового окна ключей требуется ввести пароль.
- Фальшивые выходы теперь помечаются в продвинутом диалоговом окне подтверждения транзакций.
- В различные окна сообщений добавлена кнопка Open Link (Перейти по ссылке), если такое окно содержит какую-либо ссылку.
- Обновлён жёстко закодированный список узлов: добавлено больше высокопроизводительных узлов и удалены нерабочие узлы, а также скрытые службы из v2.
- Контакты: добавлена возможность переключения столбцов имени и адреса.
- Добавлена возможность очистки списка недавно открытых кошельков.
- Размер образа приложения уменьшен на 22% (с 31 до 24 Мб).
- Размер отдельного двоичного файла Linux сокращён на 35% (с 76 до 49 Мб).

_**Исправления**_:
- Исправлена ошибка, из-за которой программа запуска оставалась открытой после открытия кошешлька.
- Флаги командной строки --stagenet и --testnet снова работают.
- При закрытии кошелька программа запуска более не зависает.
- Исправлена проблема, из-за которой кошелёк не открывался в случае отсутствия кеша кошелька.
- Внесены минимальные доработки в UI.

---

_Источник: [Feather Wallet Beta-8 released: Trezor, webcam Qr scanner, multi-input sweeps & more](https://www.reddit.com/r/Monero/comments/oiadja/feather_wallet_beta8_released_trezor_webcam_qr/)_

_Перевод: [Mr. Pickles](https://t.me/v1docq47)_  
_Коррекция: [Kukima](https://t.me/Kukima)_