---
title: "Часто задаваемые новичками вопросы о майнинг-пулах, шарах и сложности"
categories:
  - "Руководства"
thumbnail: "/img/manuals/beginner-faq-about-mining-pools-shares-difficulty/01.jpeg"
comments: false
authorbox: false
pager: true
toc: true
mathjax: true
sidebar: "right"
---

## _Часто задаваемые новичками вопросы о майнинг-пулах, шарах и сложности_

Несколько месяцев назад я читал о пуле Coinhive и о том, как масштабно и с какой лёгкостью он подвергся поруганию с точки зрения информационной безопасности, а чуть позже я был заинтригован проектом Monero. Особенно меня заинтересовало то, как управляется проект: его прозрачность, сообщество, цели, такие как противодействие ASIC-майнингу... Monero показалась мне криптовалютой для хороших парней. А затем я начал читать о Monero больше. Как бы то ни было, без дальнейших предисловий я начну задавать вопросы, которые смутили меня, и сам же буду на них отвечать.

![02](/img/manuals/beginner-faq-about-mining-pools-shares-difficulty/02.jpeg)

_Китайские и русские ASIC-майнеры Bitcoin, приблизительно 2019 год​_

## _Перед тем как перейти к самим майнинг-пулам — как на деле работают майнеры?_

**Первый шаг**: создаётся _ЗАГОЛОВОК БЛОКА (BLOCK HEADER)_

**Второй шаг**: при помощи SHA256 _ЗАГОЛОВОК БЛОКА_ хешируется и производится проверка, находится ли полученное значение ниже _ЦЕЛЕВОГО (TARGET)_. Если да, то вы выиграли в лотерею! Если нет (что и случается практически всегда), вы меняете 4 последних байта _(НОНС — NONCE) ЗАГОЛОВКА БЛОКА_ и пытаетесь снова.

## _Пытается ли майнер угадать единственное значение?_

_НЕТ_. Это было бы практически невозможно. Вероятность бы составила 1 / 2224. Майнер пытается достигнуть любого значения, которое будет ниже _ЦЕЛЕВОГО_. Например, в ноябре 2019 ЦЕЛЕВОЕ значение составляло примерно 13 триллионов (12 973 235 968 799). Таким образом, майнер выигрывает в лотерею, если находит любое из 13 триллионов значений, находящихся ниже _ЦЕЛЕВОГО_.

## _Что такое СЛОЖНОСТЬ?_

Если упростить, это отношение будет выглядеть так: _2224 / ЦЕЛЕВОЕ_ значение. Таким образом, согласно обратному отношению, чем ниже целевое значение, тем выше сложность.

По сути, сложность является иным представлением целевого значения, позволяющим обычным людям понять, что это. Ирония состоит в том, что у меня ушло немало времени на то, чтобы понять, что это.

## _Что насчёт НАЧАЛЬНЫХ НУЛЕЙ (LEADING ZEROs)?_

Это очередной способ упростить представление целевого значения или сложности. Например, у значения, которое приводится ниже, 14 начальных нулей:
```
0000000000000083ee9371ddff055eed7f02348e4eda36c741a2fc62c85bc5cf
```

Ещё одно значение той же длины с 16 начальными нулями
```
0000000000000000ee9371ddff055eed7f02348e4eda36c741a2fc62c85bc5cf
```

будет числом меньшим, чем первое, по крайней мере в 24 раза.

Следовательно, чем меньше _ЦЕЛЕВОЕ_ значение, тем выше _СЛОЖНОСТЬ_.

## _Помогают ли майнеры, входящие в пул, друг другу в решении задачи?_

НЕТ. Майнеры не помогают друг другу «решить задачу». Каждый майнер пытается решить одну и ту же задачу снова и снова. **Прогресс отсутствует**. Майнинг в пуле — это трата денег на покупку большего количества билетов для участия в лотерее.

## _Что делает МАЙНИНГ-ПУЛ?_

- Майнинг-пул создаёт ЗАГОЛОВОК БЛОКА и распространяет его среди майнеров, и в результате майнеры могут попытаться решить **одну и ту же задачу**.
- Затем пул проверяет результаты, представленные майнерами, и, когда придёт время, раздаёт _ШАРЫ (SHARES)_, следя за тем, что бы _ВОЗНАГРАЖДЕНИЕ (REWARD)_ было поделено справедливо.
- Когда блок будет вычислен, пул создаст новый ЗАГОЛОВОК БЛОКА и снова раздаст его майнерам.
- Если блок вычисляется пулом, он делит вознаграждение среди майнеров в соответствии с выбранным методом вознаграждения (пропорционально, PPLNS, SMPSS, PPS).

## _Что такое ШАРЫ?_

Доказательство работы для _ПУЛА (POOL)_. **Не имеет фактического значения**. Используется двумя способами:
- как метод подсчёта для честного дележа вознаграждения;
- для простоты доказательства того, что вы фактически пытаетесь решить задачу для ПУЛА.

Считаю, что с точки зрения механизма работы пула эта система просто гениальна, поскольку без неё не работала бы вся схема, а само решение представляется интуитивным и автоматизированным. Использование одного доказательства работы для всех майнеров в пуле помогает одновременно решить проблему самого доказательства работы и вопрос распределения добычи при **нулевых непроизводительных издержках**. Как?

Если вы пытаетесь заниматься майнингом в пуле, вы используете _ЗАГОЛОВОК БЛОКА_, созданный пулом. Проблема состоит в том, что любой результат, который вы предоставляете пулу, чтобы доказать, что вы пытались решить задачу для пула, требует подтверждения того же объёма вычислений. Если бы менеджеру пула приходилось производить тот же объём вычислений, что и майнерам, то в чём была бы выгода? Это был бы полный провал, так ведь? Как пулу узнать, что майнеры действительно работают? Как ему узнать, насколько усердно работает каждый из майнеров?

И тут в дело вступает механизм ШАРЫ. Этот механизм предполагает, что в среднем для достижения значения ниже ЦЕЛЕВОГО вы, например, в 216 раз с наибольшей вероятностью найдёте значение ниже (_216 * ЦЕЛЕВОГО_ значения). Таким образом, вместо того чтобы отправлять полностью все результаты ваших вычислений, вы высылаете только те, которые ниже _(216 * ЦЕЛЕВОГО значения)_, а пул, после того как подтвердит ваши результаты, выдаст вам _ШАРУ_.

Тому, кто предоставляет результаты с более высокой СЛОЖНОСТЬЮ, пул даст большую ШАРУ, пропорциональную уровню СЛОЖНОСТИ, так как такой результат получить сложнее, что свидетельствует о том, что вы проделали больший объём работы.

Обычно пулы предварительно задают пороговое значение сложности ШАРЫ. Также некоторые пулы, как правило, дают большие ШАРЫ за более высокий уровень сложности, так как такие майнеры дают меньше результатов и в конечном счёте требуют меньшего объёма вычислений для их валидации.

Также эта гениальная система снизить сетевой трафик между «рабочими» и пулом. Оборотной стороной является утрата точности.

Если вы задаёте более высокий порог сложности, то вы редко получаете результат. В конечном счёте результаты будут приходить редко, а майнеры не будут получать никаких ШАР.

## _Могут ли майнеры, нашедшие результат, оставить вознаграждение себе?_

**Нет, не могут**. _ЗАГОЛОВОК БЛОКА_, используемый майнерами, указывает на кошелёк менеджера майнинг-пула, откуда и будет получено вознаграждение. А результат действителен только для этого конкретного ЗАГОЛОВКА БЛОКА. Так что на практике все майнеры занимаются майнингом для менеджера пула.

## _Может ли майнинг-пул украсть вознаграждение?_

Конечно же, **ДА**! Майнинг-пул может не передать фактическую валюту в кошельки майнеров, и в этом случае нет ничего, что смогло бы заставить его сделать это. Вместе с тем всегда существует какой-либо верхний порог, ниже которого вы не сможете вывести заработанное, и многие майнеры, покинувшие пул, просто оставляют в нём свою валюту. Так что очень важно выбрать правильный пул.

Вот такие часто задаваемые новичками вопросы волновали и меня. Если вдруг вспомню, я опубликую и другие вопросы. Также мне хотелось бы услышать ваши вопросы любого уровня!