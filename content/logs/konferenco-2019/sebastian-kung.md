---
title: Безопасное развёртывание жизненно важного программного обеспечения
lead: "Себастиан является студентом-физиком Цюрихского университета и работает в компании, занимающейся разработкой аппаратных кошельков. Также он помогает различным связанным с криптовалютами проектам."
tags:
  - "Konferenco"
pager: true
sidebar: "right"
widgets:
  - "recent"
  - "taglist"
---

{{< youtube id="jOMenF5B1IY" autoplay="false" >}}

---

_**Спикер - Себастиан Кунг**_

_**Аннотация выступления**_

Подделка очередной версии Monero может иметь катастрофические последствия. Распространённые методы обеспечения безопасности новых версий, такие как публикация подписанной контрольной суммы двоичного файла, не обеспечивают защиты от атак методом возврата к старой версии, от того, что вы не получите двоичного файла с вредоносным кодом, или просто от того, что пользователи не станут проверять подписи. Я собираюсь представить вашему вниманию введение в воспроизводимые сборки, межплатформенные тулчейны, системы обновления и удобные методы верификации, обеспечивающие целостность двоичных файлов.

_**Стенограмма выступления:**_

_**Себастиан:**_ Итак, мы будем говорить о развёртывании программного обеспечения (ПО), воспроизводимых сборках, а затем я прокомментирую, почему воспроизводимых сборок уже недостаточно. Почему нам нужны системы получше.

Я также расскажу о развёртывании ПО в рамках модели, предполагающей реализацию «восходящих» версий. Итак, в случае с Monero при выпуске версии разработчик ставит метки в различных точках программного обеспечения, затем компилирует его и публикует. Таким образом, если всё пойдёт идеально, он запустит красивый космический корабль, но с точки зрения пользователей он, возможно, просто выстрелит. Как мне вернуться? Со стороны пользователей покажется, что он создал большую, давно знакомую и трудно решаемую проблему. Итак, вопрос: как нам проделать путь от исходного кода до программы, которая будет работать на машине пользователя?

У нас имеется исходный код, который мы компилируем, используя тулчейн, GCC, LLVM или какой-нибудь проприетарный тулчейн, а затем публикуем результат либо в магазине приложений, веб-сайте вроде SourceForge или на каком-нибудь другом самодостаточном сайте. Теперь, если вы публикуете ПО с закрытым исходным кодом, то всё очень и очень просто. По сути, всё, что вам нужно сделать, так это скомпилировать и опубликовать его где-нибудь, где у вас будет надёжная репутация, собрать группу пользователей, а потом сделать так, чтобы они стали использовать ваше ПО, и вы смогли заработать на этом денег.

Очевидно, что это сильно упрощённая система, представляющая собой нечто, что, вероятно, не понравится ни одному человеку в этой комнате, поскольку пользователю придётся полностью довериться двоичному объекту, который он получит. Он не сможет просто продать, украсть или каким-то другим образом повредить данные, чтобы программа делала именно то, что было указано её автором, что наиболее важно — он не сможет спокойно изучить, поправить или поделиться никаким из аспектов программы.

Ему также придётся полностью довериться тому, кто опубликовал программу, поверить, что автор не валял дурака. Так, например, если вы публиковали что-то на SourceForge, скажем, лет пять назад или около того, то в установщик для Windows было бы встроено рекламное ПО, и пользователи в результате получали не то программное обеспечение, которое собирались получить. Также мы являемся проектом, который продвигается сообществом, но мы не можем целиком и полностью доверять сообществу, даже несмотря на то, что все мы, очевидно, стремимся к достижению идеального качества создаваемого нами программного обеспечения.

В случае со свободно развёртываемым ПО, когда пользователь может изучить, изменить, поделиться и повторно опубликовать его по собственному желанию, он, очевидно, также может опубликовать изменённую версию программного обеспечения, которое будет включать в себя зловредное или рекламное ПО. Самым простым и очевидным решением, как и делается, как и делалось до последнего времени в Monero, является публикация двоичных файлов с подписью разработчика с последующей проверкой, входит ли этот разработчик в какую-нибудь доверенную сеть. При этом он может быть публичной персоной, или же он может использовать сильную PGP программу, или же что вам угодно в рамках выбранной вами скрытой модели. На Getmonero.org также имеются очень простые инструкции, как проверить это. И файл со всеми этими хешами выглядит примерно так, поэтому, по сути, довольно просто проверить, имеет ли полученный вами файл верную контрольную сумму.

Но вопрос остаётся открытым: как нам позаботиться об обновлениях? Так в магазинах приложений, например, вы получаете обновления более или менее автоматически. Разработчик может только опубликовать новую версию в таком магазине, и ваш телефон обновит приложение автоматически. С другой стороны, в случае с Monero у нас есть система обновлений, но нам необходимо быть уверенными в том, что она будет проверять странности вроде повторного использования старых версий, когда проверка подписей по-прежнему будет действительной, но при этом будут использованы эксплойты, которые могут представлять опасность для пользователя. Таким образом, нам надо что-то делать с этими токсичными отходами.

Обычно это делалось через The Update Framework или сокращённо TUF. И тут довольно точно описано, как безопасно развёртывать обновления. Красивое программное обеспечение с закрытым исходным кодом, скомпилированное ПО, просто скрипты, что угодно. По сути, пользователь ведёт записи контрольных сумм двоичных файлов, подписей и версий в отдельном файле. Этот отдельный файл не [неразборчиво] отдельно от фактического двоичного файла. Затем проводятся проверки на предмет наличия атак, на отсутствие изменения масштаба времени, и это обеспечивает разумный уровень безопасности. Система обновления Monero также была оценена относительно TUF в Monero Выпуск №4958. Пожалуйста, взгляните на это, Jasonhcwong, продюсер блоков Monero, сделал действительно замечательные замечания по этому вопросу.

Затем, более или менее [неразборчиво] относительно TUF, Monero также использует dnssec с дополнительным резервированием на случай защиты от атак подмены, когда вам доступно автоматическое обновление.

А сейчас я собираюсь сделать небольшое отступление и поговорить о статическом и динамическом связывании скомпилированного ПО. Итак, большая часть программного обеспечения, которое переносится в Debian, например, переносится как динамический двоичный файл. Это подразумевает загрузку необходимых библиотек из системы во время работы. Вы можете до некоторой степени свободно менять местами эти совместно используемые библиотеки, на которые у вас [неразборчиво] исполняемые ссылки. Они следуют общему ABI. Так, например, если вы публикуете двоичный файл через Debian, используя приложение, например, monerod, а затем проверяете зависимость гибких ссылок, вы можете сделать это при помощи ldd, и получите полный список зависимостей. Это также обеспечивает некоторую прозрачность, поскольку по факту вы видите, что разработчик использовал для компиляции вашего исполняемого файла.

Но тут, безусловно, есть важная обратная сторона. В основном дело заключается в том, что вам приходится самостоятельно управлять всеми этими совместно используемыми библиотеками, и если одна из них будет отсутствовать, ваш исполняемый файл не будет работать надлежащим образом. Это также касается отсутствующих [неразборчиво], несоответствия версий и так далее. И если вы развёртываете, например, такое приложение, как monerod, в Windows, вам придётся напрямую включить все библиотеки вместе с двоичным файлом. Таким образом, это несистемные зависимости, которые не обновляются регулярно в Windows, поэтому вы можете полагаться на Windows, когда патчите для себя ваши зависимости. Так, например, если в OpenSSL есть эксплойт, monerod придётся перекомпилировать всё и перенести это в новую версию OpenSSL.

Итак, в целом компоновка потребует очень много работы, так как вы будете делать это из расчёта на самые разнообразные операционные системы и обслуживать причуды всех этих систем управления пакетами. Существуют некоторые решения, позволяющие создавать пакеты внутри, я бы назвал это, крохотной файловой системой, подобной NAP-образу, но, опять же, и у них есть свои компромиссы. Таким образом, если вы, например, генерируете NAP-образ, вы получаете один двоичный файл, но в этот один двоичный файл будут упакованы совместно используемые библиотеки. Таким образом, вы снова сталкиваетесь с проблемой, когда при наличии эксплойта в одной из зависимостей вам придётся всё снова полностью обновлять.

Итак, поскольку у нас возникает такая проблема при переносе в Windows, статическое связывание оказывается такой же опцией. При статическом связывании библиотеки встраиваются напрямую в исполняемый двоичный файл, который вы переносите. И тогда это, по сути, решает проблему. Но если вы производите статическую компиляцию в Linux, то нужно быть немного осторожнее. По сути, это хак, и я не стал бы говорить об этом, как о чём-то широко применяемом разработчиками, работающими с Linux, но когда вы связываете двоичный файл в Linux, он также будет автоматически связываться в libc. И это всегда будет динамическим связыванием. У libc есть особенность, которая заключается в том, что эта библиотека всегда совместима снизу вверх, поэтому в новой версии libc будет работать двоичный файл, скомпилированный в системе с более старой версией libc, но не наоборот. И это решается путём повторного определения символов, используемых в родных системах внутри вашего исходного кода, когда вы производите компиляцию, и путём проверки, с какой версией glibc работает ваш двоичный файл, для этого достаточно использовать objdump -p. И как только это будет сделано, вы сможете использовать objdump -T, а затем имя двоичного файла и команду grep для той версии libc, для которой вы хотите сделать преобразование. И это делается путём повторного определения символов в исходном коде при помощи Simba таким образом, что с каждым символом, с каждым символом, простите, нарушается связь. Так, например, если у вас есть символ в версии 2.17 glibc, у него будет одна запись symver в библиотеке C. Но, когда вы начнёте поиск с возвратом к старой версии, вам снова нужно будет быть внимательным, так как они будут невосприимчивы к эксплойту. Таким образом, если вы отслеживаете версию, например, glop от версии 2.27 до версии 2.17 glibc, вы столкнётесь с этой проблемой, поскольку она была пропатчена, чтобы удалить CVE из неё, или же вам даже понадобится доступ к корню системы Linux. Если вам не удастся обойти эту проблему, то вам реально просто придётся встроить эту часть библиотеки CVE в ваш исходный код.

Я разместил пост в блоге, где было описано, как точно это сделать, и вы найдёте его, если перейдёте по QR-коду.

Итак, я сейчас говорил о том, что в целом нам следует использовать статическое связывание, если нашей целью является множество платформ. Нам известно, как развёртывать обновления более или менее безопасным способом, нам известно про контрольные суммы и подписи разработчиков, но у нас по-прежнему остаётся проблема, которая заключается в том, что если разработчик будет использовать предварительно скомпилированные библиотеки третьих сторон, эти предварительно скомпилированные библиотеки позволяют вставить вредоносное ПО в двоичный файл, который вы используете.

Решение заключается в кросс-компиляции всех ваших зависимостей из одной среды путём установки тулчейнов, необходимых для этого, на вашу хост-систему. Сейчас в Monero это делается при помощи Depends. Depends — это, по сути, система файлов сборки, автором которой является ведущий разработчик Bitcoin, Кори Филдс. Эти файлы сборки позволяют осуществлять кросс-компиляцию с Linux, Mac OS и Windows. А затем будут самые различные архитектуры, включая 32-битные, 64-битные и даже RISC-5.

Depends берёт зависимости, которые вы строите, напрямую из исходного кода, а затем проверяет их контрольную сумму, компилирует каждую из зависимостей для каждой архитектуры и операционной системы и устанавливает их в отдельную директорию, которая генерируется в среде зависимостей. И на эту директорию затем вы можете давать ссылку при компиляции вашего фактического приложения. И для этого я добавил Depends target, а затем эту архитектуру, когда мы имеем три системы, для простоты использования.

Добавить новые пакеты в Depends довольно просто. По сути, всё, что нужно, это создать новый файл для пакетов, например, здесь, например, я показываю lipsodium. Ему необходимо задать имя, версию, откуда он должен взять это из исходного кода, контрольную сумму, а затем некоторые команды, чтобы сконфигурировать его надлежащим образом, чтобы скомпилировать его правильно, а затем установить его в корень системы Depends. Многое из этого, пакеты, когда вы производите их кросс-компиляцию, требует дополнительных патчей. Этому есть ряд причин, например, в случае с lipsodium, разработчик решил, что в строке версии он вставит пробел, и если вы затем передадите это в GCC, в случае с некоторыми версиями, компилятор пожалуется на наличие этого странного пробела. Но также существует множество новых пакетов, которые совершенно устарели к моменту выхода последней версии, когда, например, 64-битные архитектуры ARM ещё даже не были как следует определены, и приходится патчить весь их исходный код, чтобы сделать их или библиотеку совместимой с ARM-64.

Теперь у разработчика есть набор безопасных библиотек, которые он может использовать для компиляции. Он может предложить пользователям более или менее безопасное обновление. Пользователи могут проверить, было ли обновление сделано достаточно безопасно, но пользователям по-прежнему приходится полностью полагаться на разработчика, на то, что он скомпилировал программное обеспечение правильно. Таким образом, когда разработчик выпускает новую версию, он может включить вредоносное ПО во время компиляции либо по собственному желанию, либо, не желая того, если кто-то взломал его систему. Как правило, когда вы компилируете или осуществляете сборку программного обеспечения в приложении, происходит две компиляции одного и того же исходного кода в двух различных системах, и вы не получите одного и того же двоичного файла. Вы получите функционал, то есть вы получите двоичный файл, который будет иметь более или менее одинаковый функционал, но контрольные суммы будут разными. Так происходит, поскольку, когда вы компилируете программное обеспечение, компилятор включает в него временные метки, системные переменные, версии зависимостей, отладочные символы и ещё многое другое, включается в ваш двоичный файл. Эта проблема решается путём запуска компиляции внутри контейнера и использованием способа, который будут всякий раз использовать абсолютно все при компиляции. Этот процесс называется воспроизводимой сборкой.

Для создания воспроизводимых сборок Bitcoin или Monero использует Gitian. Gitian, по сути, является набором скриптов, которые создают контейнер, а затем запускают сборки в соответствии с указанием разработчика внутри этого контейнера. В качестве выхода в этой виртуальной среде пользователи могут выбрать kvm, lxc или docker. А подробности сборки выбираются из dot yml файла, который вы можете пропустить через скрипты Gitian. Этот файл включает в себя все этапы компиляции, настройку времени, необходимого для сброса времени системы на ноль всякий раз, когда вы запускаете новую компиляцию и начинаете установку тулчейна.

В случае с Bitcoin и Monero в настоящее время это изначально загружается из контейнера с образом Ubuntu 18.04, и, очевидно, используется Depends для компиляции всех библиотек зависимостей. Решение по использованию Ubuntu 18.04 было принято с некоторым умыслом. Ubuntu не является самым свободным дистрибутивом, но у него есть некоторые предварительно сконфигурированные репозитории с очень современными версиями GCC. И, что более важно, он также использует APT, где оператор switch GCC компилятора в некоторой мере воспроизводимо компилируется. Как только компиляция в Gitian будет окончена, двоичные файлы скопируются обратно в хост-систему. А затем Gitian создаст этот манифест-файл, содержащий контрольные суммы использованных инструментов и библиотек, и, очевидно, двоичные файлы и приложения, которые вы создаёте. Этот файл перекрёстно сравнивается с манифест-файлами, созданными другими разработчиками, на предмет наличия определённого количества одинаковых манифест-файлов, созданных другими людьми, а затем публикуется версия.

Вот, например, несколько верхних строк манифест-файла версии 0.14.1 Monero. В них содержатся несколько новых контрольных сумм двоичных файлов Linux. Вы можете запустить Gitian самостоятельно, это довольно просто. В целом вам понадобится только установить некоторую виртуальную среду, например, docker, затем скопировать скрипт Gitian built py из репозитория Monero, а затем ввести эти две команды.

Чтобы проверить наличие источников невоспроизводимости в программном обеспечении, я предпочитаю использовать инструмент под названием Diffoscope. Просто потому что он очень-очень прост в использовании. К тому же это очень компактный инструмент. По сути, это тонкая оболочка вокруг objdump и readelf, которая просто хорошо форматирует выход. Существует множество других инструментов анализа источников невоспроизводимости, и все их можно найти на reproducible-builds.org.

Непосредственно перед тем, как нами была выпущена версия 0.14.1, был обнаружен такой источник невоспроизводимости, когда я сравнивал свой двоичный файл с файлом Говарда Чу. Единственным отличием между ними было то, что машина Говарда Чу имела несколько больше объектов в его хорошем репозитории, и короткий хеш включал в себя на один символ больше, чем в моей системе, git-репозиторий которой имел меньше объектов. Эти небольшие отличия в конечном счёте могут сильно сказаться на фактической контрольной сумме. Мы решили эту проблему, и теперь сборки Monero, наконец, воспроизводимы на каждой платформе, для которой мы создали версии.

Тем не менее воспроизводимые сборки являются недостаточной мерой, так как гарантируют только то, что все двоичные файлы будут уязвимы в равной мере. Поэтому нам необходимо потратить уйму времени на проверку каждой зависимости, которую мы используем, и, конечно же, кода, который мы пишем. Вторая проблема состоит в необходимости полного доверия к тулчейнам, которые в большинстве случаев переносятся просто как двоичный объект. Таким образом, даже если мы компилируем, например, ARCH Linux из исходного кода, нам приходится начинать с типового GC компилятора. Карл Донг очень хорошо выступил по этому поводу пару недель назад на Breaking Bitcoin. И эта общая концепция недоверия вашему тулчейну называется проблемой доверительного доверия, и впервые она была затронута Кеном Томпсоном в его докладе, когда он получил награду за работу по UNIX. По сути, проблема заключается в том, что низкоуровневые компиляторы в процессе начальной загрузки тулчейна могут перенести код в высокоуровневые компиляторы. Таким образом, может возникнуть проблема, связанная с тем, что если мы не могли начать когда-то в прошлом, скажем, где-то в 80-х, и мы начали этот процесс начальной загрузки с уязвимой версией GCC, то весь наш тулчейн мог быть уязвим всё это время, и мы не стали в результате мудрее.

Таким образом, нам нужна возможность полной изначальной загрузки нашего тулчейна. И тут в игру вступает Guix. Guix — это всё ещё новый дистрибутив Linux, создающий функциональный менеджер пакетов с тем же названием. И этот функциональный менеджер пакетов позволяет осуществлять изначальную загрузку с очень небольшим набором двоичных файлов. И прелесть состоит в том, что в какой-то момент нам будет достаточно нескольких строк ассемблерного кода с несколькими различными архитектурами, чтобы скомпилировать всю систему Linux.

Возможно, вскоре я займусь работой над интеграцией Guix и как только закончу её, развёртывание и верификация станут ещё проще, чем в случае с системой, которую мы имеем на данный момент. В сущности, необходимо будет просто запустить Linux и выполнить одну или две команды.

Перед тем как завершить выступление, мне хотелось бы поблагодарить iDunk, Говарда Чу, ph4r05, mooo и Шурэ за поддержку моей работы, которой я занимался в последние годы, и особенно Шурэ за организацию конференции.

*Перевод: [Mr. Pickles](https://t.me/v1docq47)*  
*Редактирование: [Agent LvM](https://t.me/LvMi4)*  
*Коррекция: [Kukima](https://t.me/Kukima)*