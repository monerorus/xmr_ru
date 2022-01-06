---
title: Эпизод 03 - Нулевые ложные выходы и цепные реакции
weight: 3
lead: "Саранг и Джастин обсуждают кольца с нулевыми ложными выходами (нулевыми миксинами), возможно, самый старый из известных и наиболее изученный недостаток Monero. Разговор идёт о том, как результаты исследования колец с нулевыми ложными выходами могут быть применены к другим типам анализа. Демонстрируется динамическая таблица, используемая для оценки последствий цепной реакции, которая может возникнуть в результате целого ряда возможных атак на сеть Monero. Понимание базовых принципов исследования нулевых ложных выходов позволит без каких-либо трудностей понять, как нами изучаются потенциальные последствия проведения атак и анализа других типов."
tags:
  - "Breaking Monero"
pager: true
sidebar: "right"
widgets:
  - "recent"
  - "taglist"
---

{{< youtube id="1CfXHC2IFx4" autoplay="false" >}}

*08/01/2019*

[Ссылка на электронную таблицу](https://onedrive.live.com/view.aspx?resid=473062B43FF0AD33!23780&ithint=file%2cxlsx&authkey=!AOpTq2h4tkFKeUU)  

_**Стенограмма эпизода:**_

_**Джастин:**_ Привет, и добро пожаловать в третий эпизод Breaking Monero из серии программ, в которых мы рассматриваем ограничения механизмов обеспечения безопасности и анонимности Monero доступным и понятным образом. Сегодня мы поговорим о транзакциях с нулевыми ложными выходами или о транзакциях с нулевыми миксинами, а также об эффекте цепной реакции, так что сегодня у нас как бы получается двойной эпизод. Но мы попытаемся сделать его короче двух предыдущих, чтобы немного ускорить процесс и быть более конкретными в данном случае. Итак, как обычно, с вами я, Джастин, и с нами сегодня Саранг, которому уже не терпится поприветствовать вас, так что не будем затягивать, Саранг.

_**Саранг:**_ Привет, меня зовут Саранг Ноезер, и я являюсь одним из исследователей, работающих в Исследовательской лаборатории Monero на благо сообщества Monero.

_**Джастин:**_ Прекрасно. Итак, мне бы хотелось начать со скриншота одной из презентаций, которая была сделана мной для конференции Defcon, где я рассказывал, в частности, об этой особенности кольцевых подписей. Сейчас я его покажу, OK. Итак, слева на экране можно увидеть кольцевую подпись. Всё, что показано в зелёном овале. Это как бы все потенциальные выходы, которые могут быть отправлены при проведении транзакции Monero. Скажем, вот этот вот золотой, вот этот золотой, на котором я держу курсор, является тем, который действительно тратится, а следовательно, образ ключа принадлежит ему. А все вот эти позолоченные — это выходы Monero, которые потенциально могут быть потрачены. Транзакции с нулевыми ложными выходами — это транзакции, которые проводятся вообще без каких-либо выходов, которые потенциально могут являться тем, который реально тратится. Поэтому, когда вы сталкиваетесь с такой транзакцией, вы точно знаете, какой выход тратится. Тут вы можете увидеть пример. Предположим, это очередная транзакция с нулевым количеством ложных выходов и размером кольца равном единице. Так как в состав кольца входит только один выход, то вы точно знаете, что именно этот выход тратится. Так что вы можете сказать: «OK, так как этот выход тратится здесь, то я могу просмотреть все остальные транзакции, в которые он входит», а потом: «эй, этого выхода не может быть там», как в этом примере, где кольцо включает в себя этот выход. Таким образом, вы смело можете поставить крест на этом выходе и сказать: «этот выход не может быть потрачен», а если ситуация повторится с несколькими другими транзакциями, у каждой из них будет свой собственный набор нулевых ложных выходов. С другой стороны, это старые транзакции Monero, которые проводились на раннем этапе, в 2014 и 2015. И вы можете видеть, что если каждый отдельный выход появляется в другой транзакции с нулевыми ложными выходами, то вы можете понять, что один из выходов тратится по факту. При наличии только одного вероятного выхода, который может быть потрачен, кольцевая подпись может быть вскрыта. Это основа для проведения атаки или для анализа на базе использования нулевых ложных выходов. Вы просматриваете транзакции с единственным возможным выходом траты и сравниваете их с другими транзакциями, чтобы получить информацию, то есть как бы обтесать, сузить объём информации. И вот с этого момента, когда уже известно, что выход был потрачен конкретно вот в этой транзакции, он уже обозначен жёлтым цветом, и любая другая транзакция может включить такой выход, например, как если бы этот выход был создан как tx10. После этого мы можем убрать его, как показано в случае со второй кольцевой подписью, и вот справа мы уже получаем эффект распространения. Этот эффект распространения называется «цепной реакцией». Таким образом, что на самом высоком уровне этот график может помочь понять идею проведения атак и анализа транзакций с нулевыми ложными выходами Monero, а также отразить принцип цепной реакции, возникающий из-за транзакций с нулевыми ложными выходами. Как тебе, Саранг?

_**Саранг:**_ Да, так оно и есть. То есть как я представляю себе итеративный процесс, то он подобен чистке луковицы. Это не точная аналогия, поскольку это не совсем похоже на луковицу. Но в целом идея была правильно изложена тобой: ты повсюду ищешь транзакции с нулевыми ложными выходами, ищешь, где ещё появятся их выходы, а затем ты просто начинаешь «очищать» другие кольца и в конечном счёте ты можешь получить кольца, которые станут транзакциями с нулевыми ложными выходами, и ты уже берёшь их и повторяешь процесс итеративно с кольцами большего размера. То есть ты прав, вся идея состоит в итеративном нахождении транзакций с нулевыми ложными выходами, используя свойство таких транзакций, которое заключается в том, что те выходы, которые тратятся, известны. И, конечно же, в случае с Monero общая задача состоит в том, чтобы мы не знали, был потрачен выход или нет, поскольку в противном случае получается недействительный ложный выход для включения в большие кольца в будущем.

_**Джастин:**_ Итак, транзакции с нулевыми ложными выходами были запрещены в Monero, если я не ошибаюсь, в марте 2016, правильно?

_**Саранг:**_ Возможно. Кажется, я пропустил этот момент.

_**Джастин:**_ Но в период между тем, как минимальный размер кольца Monero был увеличен, и до появления RingCT в начале 2017 по-прежнему можно было наблюдать, как проводился анализ транзакций с нулевыми ложными выходами, хоть и в меньшей степени… но он также имел измеримые последствия. По-прежнему о транзакциях можно узнать многое. И такой анализ был также возможен, несмотря на то, что уже никто не мог осуществлять такие транзакции.

_**Саранг:**_ Конечно. Опять же, вся идея состоит в интерактивности. Точно. Когда ты можешь взять ранние транзакции и отсечь всё, что может быть ложными выходами, чтобы добраться до настоящей траты. Можно протолкнуть их в меньшие кольца, а затем понемногу и в большие. Ну, по мере того как размер кольца будет становиться больше. Фактически количество выходов, которые ты как бы можешь отсечь от больших колец, в конечном счёте становится менее эффективным. Опять же, вот одна из причин, почему с увеличением размера кольца такой анализ становится менее эффективным. Это своего рода дополнительные меры предосторожности. Ты как бы добавляешь больше ложных выходов, чтобы ослабить эффект распространения. Эффективность сохранится в некоторой степени, но со временем уровень эффективности тех выходов сойдёт на нет. Частично дело обстоит так из-за способа выбора ложных выходов, а мы реально не обсуждали, как точно это делается, мы просто используем слово случайно… как-то не обсуждаем это… это должно измениться со временем, и я уверен в том, что мы ещё поговорим в каком-нибудь будущем эпизоде конкретно о том, как выбираются выходы из блокчейна, и почему это важно, когда речь заходит о ложных выходах. Однако достаточно сказать, что со временем мы стали улучшать процесс выбора выходов, и этот вид анализа стал уже не таким эффективным, как раньше.

_**Джастин:**_ Превосходно. Спасибо. Не мог бы ты немного рассказать об истории обнаружения Monero нулевых ложных выходов такого рода. Мне известно, что есть исследовательские работы, [MRL-0001](https://web.getmonero.org/resources/research-lab/pubs/MRL-0001.pdf) и [MRL-0004](https://web.getmonero.org/resources/research-lab/pubs/MRL-0004.pdf), в которых излагалась идея цепных реакций, то есть исследовательские работы касались непосредственно этой проблемы.

_**Саранг:**_ Да, так и есть.

_**Джастин:**_ OK. Ты говорил, что есть новая исследовательская работа или, по крайней мере, относительно новая статья, которая поможет оценить проблему немного лучше?

_**Саранг:**_ Да-да. Идея уже витала в воздухе какое-то время. Она обсуждалась, и в итоге появилось два внутренних документа MRL 1 и 4, проблема обсуждалась с разных сторон, кто-то говорит, что это некоторого рода случайный пассивный анализ, а кто-то считает, что это активный анализ… перспективный… то есть кто-то намеренно вбрасывает выходы в блокчейн, то есть понимает, что делает, так что на проблему можно взглянуть с нескольких сторон. Но та мера, в которой это фактически делалось в последней версии блокчейна, реально не оценивалась вплоть до появления пары работ, одна из которых вышла под двумя разными названиями, первое название препринта немного отличалось, но появившийся позднее, в апреле 2017, препринт носил название [«Эмпирический анализ: отслеживаемость в блокчейне Monero»](https://arxiv.org/abs/1704.04299). А потом вышла ещё одна работа, которая имела похожее название, [«Анализ отслеживаемости в блокчейне Monero»](https://eprint.iacr.org/2017/338.pdf), что внесло некоторую путаницу, но это пошло на пользу, позволив говорить о нескольких различных формах анализа, а также количественно оценивать эти формы анализа, какие результаты они дают, а также примерные цифры за некоторый период. Стало известно, что где-то около 65% выходов Monero отслеживалось при помощи некоторой комбинации нулевых миксинов, цепной реакции… возможно, пара других форм анализа… что, я должен сказать, звучит очень, очень пугающе, как «Боже, если можно узнать 65% потраченных выходов и их нельзя выбирать для современных транзакций, конечно же, я, да и любой другой попадает в довольно стеснённые обстоятельства». Но опять же, учитывая то, как мы выбираем выходы, со временем очень, очень маловероятно позволит выбирать эти выходы, а позже ещё во многих работах повторно рассмотрены эти формы анализа. Знаешь, через какое-то время мы увидели целый ряд работ, в которых были описаны одна или две новые небольшие формы такого анализа, но по какой-то причине в них была снова и снова отражена вот эта идея цепной реакции как части анализа, в результате это, как мне кажется, привело к неправильному толкованию того, что уже было известно о цепной реакции, к сожалению. Поэтому нами фактически было проведено совершенно независимое исследование, чтобы увидеть, можем ли мы воспроизвести эти значения, была написана работа [MRL-0007](https://web.getmonero.org/resources/research-lab/pubs/MRL-0007.pdf), в которой мы представили другую, более общую форму анализа, и нам удалось получить приблизительно те же цифры, и если взглянуть на блокчейн в целом с любой точки, с которой смотрели они, вплоть до начала истории Monero, то точно также выяснится, что было известно примерно 65% потраченных выходов, что и показал этот анализ. Но если посмотреть на современные транзакции, в частности, на те, что были созданы после большого перехода на RingCT, то становится ясно, что они исчезают. То есть я хочу сказать, что на тот момент, когда мы обнаружили это, нулевые выходы были уязвимы к этому виду анализа. И если вы выбирали старые выходы, которые уже были проанализированы, то это было скверно, но в случае с современными транзакциями такого уже не происходит.

_**Джастин:**_ Точно. Я думаю важно, что в прошлом эпизоде мы говорили об идее правдоподобного отрицания. Транзакции с нулевыми ложными выходами являлись важной темой, достойной рассмотрения, поскольку это разрушало идею правдоподобного отрицания, связанную с транзакциями Monero, поскольку достаточно было взглянуть на информацию, которая хранится в блокчейне Monero, чтобы определить, что выход был потрачен при проведении вот этой транзакции, и более нигде он уже не мог быть потрачен. Поэтому этот вопрос и был важен. И я рад слышать, что у нас есть ответы на него. На данный момент у нас есть несколько исследовательских работ по теме, но важно при этом различать Monero до появления Ring CT и после появления Ring CT, поскольку это как день и ночь.

_**Саранг:**_ И тут стоит отметить, что в современных транзакциях по большей части используются только Ring CT выходы лишь за минимальными исключениями. Те транзакции, которые используют выходы, сгенерированные до реализации RingCT, предположительно являются транзакциями, которые мы относим к некоторой категории… и прочее. Они не выбираются. Поэтому во многих работах не приводилось чёткого разделения, и мне кажется, что именно поэтому какое-то время так мутили воду вокруг этих 65%.

_**Джастин:**_ Есть ли что-то ещё, что тебе хотелось бы сказать о нулевых ложных выходах, или ты хотел бы сейчас сфокусироваться на идее цепных реакций, которые остаются тем, что нами было оценено как очередной вектор атаки, а также на том, как эти методы вызова цепной реакции могут сказаться на Monero, поскольку мы более не рассматриваем нулевые ложные выходы или нулевые миксины, поскольку эта проблема как бы удаляется от нас.

_**Саранг:**_ Нет, всё правильно. То есть, честно говоря, идея нулевых миксинов лежит в основе идеи цепных реакций, поскольку мы получаем такой вот вид «луковой методологии», пытаясь разделать транзакции, но мы поговорим ещё в следующих эпизодах о других методах анализа, позволяющих определить, были потрачены выходы или нет. И идея цепной реакции будет применима после проведения таких видов анализа. Так что, возможно, я смогу определить какими-то другими способами, был или нет потрачен ряд выходов посредством моей новой формы умного анализа (каким бы он ни был). И улучшений со временем не ожидается. Вы так же можете взять те выходы, которые, как вам известно, были потрачены. Они явно будут из транзакции с нулевыми миксинами, и, используя их, вы сможете запустить цепную реакцию. Так что в целом пока мы можем идентифицировать некоторые современные выходы как потраченные, мы сможем как бы удалять их из других современных транзакций. А смысл цепной реакции состоит в том, чтобы делать это в достаточном объёме для того, чтобы сократить очередное большое кольцо до одного остающегося выхода. И в целом мы не в состоянии сделать подобного, что хорошо. Возможно, в какой-то из транзакций и получится удалить один, два или даже большее количество выходов, чем рассматривается нами. Но при этом их не хватит, чтобы сократить кольцо до одного выхода. Принцип правдоподобного отрицания будет действовать по-прежнему.

_**Джастин:**_ Отлично. Я думаю, действительно важно принимать во внимание идею нулевых ложных выходов и нулевых миксинов, поскольку если ты можешь воспроизвести подобный принцип, который применяется в отношении нулевых ложных выходов, нулевых миксинов и который довольно прост для понимания, то ты можешь сделать это для проведения гораздо более сложных атак, воссоздавая ситуацию с такими нулевыми ложными миксинами и нулевыми миксинами. Поэтому мне кажется, будет важно поделиться со всеми расчётами, которые я покажу тебе и которые позволят оценить эту цепную реакцию и увидеть, при каком состоянии сети и при каком множестве раскрытых выходов можно также будет «вскрыть» другие транзакции. Так, сейчас. Я использую [эти расчёты довольно часто](https://onedrive.live.com/view.aspx?resid=473062B43FF0AD33!23780&ithint=file%2cxlsx&authkey=!AOpTq2h4tkFKeUU). Я использую эти расчёты довольно часто. Я сделал их в начале 2018, чтобы людям было проще понять ситуацию. По сути, это расширение работ MRL 1 и 4. Тут нет никаких новых идей. Эти расчёты действительно просто использовать. Тут всё реально просто: задан размер кольца равный трём, и это совсем небольшой размер, но он был первым обязательным размером для Monero, вот — три… и можно увидеть, что четыре слева имеют другую пропорцию раскрытых выходов. Поэтому они варьируются между нулём и технически не 100 процентами, но почти 100 процентами, и вы видите пропорцию времени, в течение которого открывается истинный вход, то есть в течение которого вы можете взломать эту кольцевую подпись. Так что здесь вы можете непосредственно наблюдать эффект цепной реакции. Вы также можете сказать: «OK, половина выходов раскрыта», допустим, половина выходов является нулевыми ложными выходами. Затем вы можете продолжить: «OK, тогда для двадцати пяти процентов готовых транзакций проведём анализ на этом уровне», после чего вы и они будут вскрыты, и тогда вы скажете: «OK, теперь у нас есть эти двадцать пять процентов вскрытых выходов», запустим тест повторно, включив в него эти двадцать пять процентов. И это можно делать на нескольких уровнях до тех пор, пока у вас не получится конечная сумма, соответствующая всем этим указанным выходам. Вот тут в последней колонке приводится общая пропорция всех выходов, которые были раскрыты под воздействием цепной реакции. Таким образом, если у вас возникла ситуация, при которой 50 процентов выходов раскрыты и являются действительными, то при определённых обстоятельствах вы можете продолжать тесты и таким образом нарушить целостность других двадцати пяти процентов выходов, и общая сумма составит примерно 80 процентов от общего количества выходов, которые будут известны некоему внешнему лицу, проводящему атаку. Эти цифры, на самом деле, не значат ничего, но большее количество раскрытых выходов означает более масштабную цепную реакцию. В этом смысле я как бы складываю их вместе, чтобы можно было увидеть, что я использую меньший размер кольца. Давайте возьмём текущий размер кольца Monero, равный одиннадцати. Цепная реакция становится очень, очень слабой. Так у вас теперь гораздо меньшее число, чем было до этого. Это относительное понятие. Вот уже 0,01, хотя до этого оставался один знак до 4. И снова это число не значит ничего. Это просто число, с которым можно сравнивать другие размеры кольца. Но в конечном счёте можно увидеть, что для любой определённой суммы эффект первого порядка будет всё более незначительным. Даже в случае нереально большого количества раскрытых выходов при большом размере кольца. И если мы возьмём какой-то невероятный размер кольца, равный 100, например, или какой-то другой, то мы увидим, что цепная реакция станет неизмеримой, чтобы значительно повлияет на другие транзакции. Поэтому я просто собираюсь быстро показать разницу между размерами колец Monero, равными 3 и 11, что показано на графике справа, внизу справа, где показано соотношение известных раскрытых выходов, с которого всё начинается. А по оси y показано соотношение транзакций, которые были раскрыты, или соотношение раскрытых колец. И тут, в случае с размером кольца, равным 3, видно, что оно защищено гораздо меньше, чем кольцо с размером, равным 11. И так как размер кольца становится всё больше и больше, кривые смещаются всё дальше и дальше вправо и становятся всё круче, поскольку цепная реакция уже происходит на порядок выше. Вот что Саранг и я имели в виду, когда говорили, что размер кольца при проведении транзакций должен быть большим, так как для вызова цепной реакции в сети Monero понадобится на порядок больше выходов. Я считаю, что этот ресурс может помочь нам количественно оценить то, что мы называем цепной реакцией. Опять же, она не обязательно затронет именно нулевые ложные выходы, это может быть любое соотношение выходов, на которые она повлияет, и мы можем провести ряд тестов, касающихся информации, которую мы включим в эту таблицу Excel, которую лично я считаю довольно полезной.

_**Саранг:**_ Да, и эти цифры действительно ничего не значат, если мы знаем, что современные транзакции по большей части не подаются какому-либо из видов такого анализа. Фактически у нас есть инструмент, который является частью Monero, встроенный в набор инструментов. Мы называли его «инструментом отрицательного отбора» (blackballing tool). Мы поняли, что название несколько вводит в замешательство. Я считаю его просто инструментом поиска потраченных выходов. Он позволяет вам сделать собственную копию блокчейна и проводить различные виды анализа, включая этот анализ на базе нулевых ложных выходов и цепной реакции, а также внутренне помечать те выходы, которые уже известны в качестве потраченных и которые не следует выбирать в качестве ложных. Этот инструмент гарантирует, что такие выходы не будут выбраны. Опять же, в случае с современными транзакциями вероятность того, что будет выбран выход, которого коснулся этот анализ, очень мала… очень-очень мала. И мы не говорили о каких-либо современных выходах, которые ещё не были сгенерированы, а только о транзакциях, в которых тратились более старые, гораздо более старые выходы, те, что появились ещё до Ring CT, но инструмент позволит избежать их выбора. Инструмент немного неэффективен, поскольку ему приходится анализировать большой объём. Но если вы возьмёте и решите подстраховаться, то инструмент поможет вам в этом.

_**Джастин:**_ Это просто моё мнение, что, в случае с большими размерами колец, этот инструмент реально помогает нам оценить, подвергается или нет сеть серьёзной атаке. То есть, если происходит разветвление блокчейна, вы можете сказать: «OK, давайте-ка оценим, что тут». Мы поговорим о разбиении позже. Этот инструмент необязателен для тех, кто просто отправляет средства, для снижения рисков, связанных с транзакциями, или даже…

_**Саранг:**_ Нет, конечно же, нет, только для транзакций с нулевыми ложными выходами и транзакциями, затронутыми цепной реакцией. Повторю: современные транзакции такому воздействию не подвергаются.

_**Джастин:**_ Отлично. Кажется, мы охватили все базовые принципы работы нулевых ложных выходов и цепной реакции. Надеюсь, эта информация будет полезна людям. Есть ещё что-то, что ты хотел бы добавить, Саранг?

_**Саранг:**_ Только то, что было проведено множество реально хороших исследований, в которых приняли участие как исследователи из внутренней, так и внешней среды, и исследования темы продолжаются, даже несмотря на то, что мы уже понимаем её в достаточной мере, но мы делаем это для исследователей, которые, возможно, не читали предшествующих работ, и мы даём им дополнительную информацию. Существует множество различных доступных статей и препринтов, и если вы имеете научную или математическую базу и хотите больше узнать о том, какой вид анализа позволил нам построить защиту от этих видов анализа.

_**Джастин:**_ Отлично. Ещё раз спасибо тебе. Спасибо, Саранг, что присоединился ко мне. Спасибо нашим зрителям за то, что смотрели этот эпизод Breaking Monero. Я рад, что он получился короче остальных и что мы охватили всю необходимую информацию и ничего лишнего. Мы постараемся сделать так, чтобы другие эпизоды были такими же короткими. На этом мы прощаемся с вами, смотрите наши последующие эпизоды и берегите себя.

*Перевод: [Mr. Pickles](https://t.me/v1docq47)*  
*Редактирование: [Agent LvM](https://t.me/LvMi4)*  
*Коррекция: [Kukima](https://t.me/Kukima)*