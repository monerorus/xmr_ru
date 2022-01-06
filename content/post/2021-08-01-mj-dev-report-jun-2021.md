---
title: "Отчёт mj за июнь по разработке и интеграциям"
date: "2021-08-01"
categories:
  - "Новости"
tags:
  - "CCS"
lead: "Ежемесячный отчёт mj в ключе работы над его CCS предложением."
pager: true
toc: false
sidebar: "right"
widgets:
  - "recent"
  - "taglist"
---

Уважаемое сообщество!

В прошлом месяце большую часть времени моя работа была сосредоточена на решении некоторых коварных проблем, связанных с CI. С одной стороны, я и @selsta убедились в том, что CI проверяет по крайней мере наиболее репрезентативные комбинации настроек сборки, а с другой стороны, я обнаружил, как часто наши кэши обрезаются из-за их совокупно большого размера, в результате чего появляется большое количество задач, а также неэффективно обработанных кэшей этих задач. Мне удалось внести соответствующие исправления и решить все эти проблемы. Поскольку кэши более не будут обрезаться так часто, скоро мы станем свидетелями более быстрой проверки CI непосредственно с первого коммита (после слияния соответствующей ветки, конечно же). Мне также удалось исправить распространённую ошибку ccache под FreeBSD, хотя изначально я не был уверен, в чём именно была причина.

Также я постепенно переношу свой отчёт на другой хост, который, надеюсь, будет менее ограничительным с точки зрения читателей по всему земному шару. Изначально отчёт размещался здесь: http://enjo.hopto.org/pub/monero/, и теперь я перемещаю его на этот адрес: http://cryptog.hopto.org/monero/health/

Пожалуйста, дайте мне знать, если у вас не получается получить доступ к какому-либо из них. Если нет, то к какому именно?

Мною был составлен новый подотчёт под названием Headers (Заголовки). Это самостоятельно разработанный, не содержащий зависимостей инструмент для статической проверки зависимостей заголовков, позволяющий приблизительно за несколько секунд проделать работу, выполняемую Clang Build Analyzer, то есть, ему не требуется для этого целого часа, необходимого CBA. Как только инструмент достигнет состояния готовности, он станет удобным и быстрым средством, которым смогут пользоваться абсолютно все, подобно отчёту LCOV. А пока я просто размещаю здесь [версию для предварительного просмотра](http://cryptog.hopto.org/monero/health/data/56f760964/56f760964-headers-result.txt), где в самом верху вы можете увидеть обычного подозреваемого, wallet2.h :)

## _Ветки_

Вот традиционный список объединённых и вновь открытых веток:

_Новые ветки_
- CI: [зависимый кэш (статический), отделённый от ccache (изменяемого)](https://github.com/monero-project/monero/pull/7780). Я обнаружил, что каждая из многоплатформенных сборок хранит статический предварительно созданный файл вместе с изменяемыми файлами ccache. Поскольку практически в каждой новой ветке появляются некоторые изменения в файлах ccache, должен создаваться и новый архив кэша, который также включал бы и статические файлы, по сути, дублируя их без какой-либо причины. Это, наконец, привело к тому, что GitHub стал обрезать наши кэши в каждой 3-4-й ветке, что заставило CI начать кэширование заново. Я разделил эти кэши на 3 категории: изменяемые (ccache), в основном статические (тулчейны) и полностью статические (OSX SDK), тем самым увеличив время жизни кэшей примерно в 3 раза.
- CI: [Ubuntu-Test повторно использует кэш Ubuntu-Build и создает статические библиотеки](https://github.com/monero-project/monero/pull/7787). Не было бы никаких причин для повторной сборки версии Ubuntu для тестов, если бы она строилась в качестве предварительного условия. В этом случае моя ошибка ранее заключалась в том, что я настаивал на динамической связи тестовой сборки, что означает появление отличной (и несовместимой) от только что созданной версии. Во-вторых, ошибка заключалась в тестировании чего бы то ни было в конфигурации, отличной от той, которую получает конечный пользователь (речь идёт о динамическом и статическом связывании, соответственно). Вместе с @selsta мы пришли к выводу, что лучше будет локально протестировать крайние случаи системы сборки. Также, поскольку, как вы только что прочитали в предыдущем пункте, мы уже достигли ограничения размера кэша, нам пришлось поддерживать показательный минимум количества заданий. Такое изменение позволяет сэкономить около получаса лишнего времени сборки.
- CI: [CCache во FreeBSD работает](https://github.com/monero-project/monero/pull/7797). Как уже упоминалось, я заставил CCache работать, проведя тщательный анализ выдачи ошибочных команд. Выяснилось, что ccache под FreeBSD не работает, потому что двоичный файл ccache ожидает двоичный файл компилятора в качестве входящего, в то время как в случае FreeBSD он загружался с помощью сценария, предназначенного для конфигурирования двоичного файла компилятора за один раз. В данном случае работа состояла в том, чтобы разделить сценарий на часть, относящуюся к компилятору, и часть, связанную с конфигурацией. Чтобы сделать решение более устойчивым относительно изменений, вносимых в рамках будущих версии, сегментация производится автоматически с использованием Regex в файле CMake.
- Doxygen: [Исключение директорий сборки](https://github.com/monero-project/monero/pull/7804). Файл конфигурации Doxygen в корневой исходной директории конфигурирован для разбиения всех репозиториев в течение некоторого времени. Тем не менее, это оставило нерешённой проблему сканирования не только очевидной директории сборки, но также и не столь очевидной директории contrib/depends, куда попадают все неинтересные файлы зависимостей, что может даже привести к сбою Doxygen, когда директория будет полностью заполнена различными многоплатформенными тулчейнами.
- utils/health: [Добавление инструментов покрытия строк](https://github.com/monero-project/monero/pull/7806). Наконец, сценарий LCOV, который я использую для генерирования моих автоматических отчётов, теперь имеет качество, соответствующее полной готовности (читай: может быть правильно конфигурирован вызывающей стороной). Это означает, что теперь каждый желающий получить быстрое подтверждение, если предлагаемые им изменения имеют положительный эффект по охвату, или же если только что написанные тесты затрагивают крайние случаи, которые должны быть затронуты, получит его. Ветка содержит подробно задокументированный пример сценария, подготовленный специально для реализации процесса разработки через тестирование. Это изменение в целом в совокупности с двумя другими подразумевает [отсутствие повторного связывания с изменением в реализации](https://github.com/monero-project/monero/pull/6937), а [динамическое связывание Epee](https://github.com/monero-project/monero/pull/7416) является последним оправданием для написания хороших модульных тестов ;)
- utils / health: [Разделение тестов Clang Tidy для C и C ++](https://github.com/monero-project/monero/pull/7808). Простая публикация небольшого, но важного локального изменения, сделанного мною и используемого для моих отчётов по двум основным причинам: во-первых, наличие ошибок одного сканирования, не влияющих на второе, и, во-вторых, возможность запускать оба сканирования параллельно.

_Незначительные изменения_
- Зависимости: [сценарий mingw32-update-gcc-posix.sh](https://github.com/monero-project/monero/pull/7779). Просто извлечение важного фрагмента кода из рабочих процессов GH, так как код также полезен и локально. Здесь также применяется некоторое сокращение дублирования. Также предоставлена документация.
- Док: [обновление статистики блокчейна комментариями](https://github.com/monero-project/monero/pull/7772). Просто обновил документацию другого человека, сопроводив её аналитическими комментариями. У этого человека не было доступа к внесению записей в репозиторий Monero, поэтому был использован такой способ «пост-априорного» обновления, позволивший избежать проблем, связанных со слиянием с исходной веткой.

_Объединённые ветки_
- EasyLogging ++: [Добавление UTests, служащих защитой от регрессий](https://github.com/monero-project/monero/pull/7771). Добавлены 2 теста, которые подтвердили валидность недавнего исправления ошибки сегментации в EasyLogging ++, сделанного moneromoo, и защитили его от регрессии. Эта ветка является одной из причин, по которой покрытие кода подскочило на 10%. Я не могу сказать наверняка, единственная это причина или нет.
- CI: [Обратная совместимость теста ubuntu 18.04](https://github.com/monero-project/monero/pull/7769). Расширение обратной совместимости с Ubuntu 18.04 с использованием пакетов, используемых по умолчанию для версии Ubuntu по результатам обсуждения проблемы с @selsta. С помощью рабочих процессов Matrix была достигнута возможность многократного повторного использования кода (процесс также известный как параметризация)

_Закрытые (не объединённые) ветки_
- Mac: [Исправление динамической привязки в устройстве](https://github.com/monero-project/monero/pull/7775). Мой приятель @TimSycamore захотел предоставить патч для исправления ошибок в динамической привязке Mac OSX, но позже выяснилось, что этот запрос уже был заменён более крупным PR, но при этом всё ещё находился в состоянии открытого запроса.
- CI: [Тестирование последней версии Boost под Ubuntu](https://github.com/monero-project/monero/pull/7770). В июле был момент, когда вышла новая версия Boost, но компиляция этой новой версии завершилась неудачно. На тот момент у меня было острое желание обеспечить возможность обнаружения подобных ошибок заранее, но позже мы решили просто ограничить количество выполняемых заданий, полагаться на конкретные PR, касающиеся исправления крайних случаев, а не на их автоматическую проверку. Кроме того, позже в этом же месяце система управления пакетами Mac OSX Brew стала автоматически выдавать последнюю версию Boost, что сделало мои изменения устаревшими.
- CI: [Матрица версии Boost для build-ubuntu](https://github.com/monero-project/monero/pull/7768). В данном случае я хотел проверить не только последнюю совместимую версию, но и самую младшую совместимую версию, и пришёл к интересным выводам, которые можно найти в описании ветки. Вкратце: самая младшая версия Boost, официально декларируемая как самая младшая совместимая версия для сборки Monero, слишком стара для создания библиотек OpenSSL, которые содержат важное исправление безопасности, вышедшее где-то в начале года. По вышеуказанным причинам мы решили закрыть ветку.

Спасибо, что прочитали мой отчёт, и за вашу непрерывную поддержку!
mj

---

_Источник: [Dev report June 2021](https://www.reddit.com/r/Monero/comments/ovtxwf/dev_report_june_2021/)_

_Перевод: [Mr. Pickles](https://t.me/v1docq47)_  
_Коррекция: [Kukima](https://t.me/Kukima)_