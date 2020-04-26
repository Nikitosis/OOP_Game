**game**

Ah, yes, game.

I suggest a mobile game, with &quot;minimalist&quot; styling. Just so that we don&#39;t have to do too much design work. (also, if we upload it to [itch.io](https://itch.io/), I can distribute it through the mobile app that I&#39;m working on).

D. P. : I agree on the idea, a mobile game would be great

**Suggested engines/frameworks:**

- MonoGame - open source, C#, simple graphics, cross-platform (desktop + mobile)
  - This is a framework, not an engine. So we&#39;ll have to builds parts of the engine on our own

**Suggested game ideas:**

- I want to flex my coding skills, and make something complicated. E. g. a sandbox game with randomly generated content. Or a (simple) multiplayer game.

Давайте думать, например, какие фичи для нас желатальные, а какие нет:

**Желательные:**

-Стоит подумать про мультиплеер. Это интересная задача с точки зрения программирования, и если есть мультиплеер, то не надо заморачиваться над искуственным интеллектом

-Было бы прикольно иметь рандомную генерацию контента

**Не желательные:**

-Хотелось бы, чтобы геймплей не требовал много контента

-Поменьше физики, т.к. это уже больше на алгоритмы (в гоночных играх, например, очень сильный упор на физику)

**Конкретные идеи:**

- Игра в жанре &quot;tower defence&quot; с мультиплеером: один игрок - защитник, другой - нападающий.
  - Думаю, мы вчетвером вполне можем сделать нормальный мультиплеер, с сервером и клиентами.
  - Хотя блин, стоп, это ж получится Clash of Clans(((
- (сюда еще идеи)

**Идея №???: упрощенный симулятор города**

**Игрок становится мэром города на какой-то срок, допустим, 20 лет.**

1. Игроку дается возможность выбрать длинну игры (например, 15 лет/30 лет/50 лет)
2. Также дается возможность выбрать &quot;сценарий&quot; города (например, нормальный город, город возле реки, город в пустыне...)
  1. Если у нас останется время (в чем я сомневаюсь), то сделаем более веселые сценарии, например, город Ухань, или город рядом с активным вулканом…
  2. Также, если останется время, то можно сделать рандомную генерацию карты. Но я думаю, что это не обязательно.

**Игра проводится в виде пошаговой стратегии** : допустим, что один год - это один ход

1. В начале хода игрок может **строить здания** , **менять их характеристики** (например, **увеличить/уменьшить бюджет больницы** ) и т.д.
2. Потом он нажимает кнопку типа &quot;End Turn&quot;, и игроку показывают последствия его решений (например, из-за того, что он уменьшил бюджет больницы, качество жизни в ближайших домах упало, из-за этого там начинают жить более бедные люди, которые платят меньше налогов)
3. Потом начинается следующий ход.

**Игра в стиле &quot;casual&quot;, а это значит:**

1. Симуляция упрощенная, графика не реалистичная (графику обсудим чуть позже, пока что решаем за геймплей).
2. Размер карты маленький, допустим, 20х20.
3. **Всю игру от начала до конца можно будет пройти максимум за час (или полчаса). Примерно как одна сессия в Plague Inc., если кто-то помнит**
4. Таким образом, нам не придется добавлять много контента, а игрок сможет испробовать несколько разных стратегий(?)
  1. Если мы таки добавим сложные сценарии городов, то можно сделать их как unlockable: открываются после первого прохождения игры.

Если бюджет уходит в минус, то Game Over. Если игрок выжил до конца срока, то он &quot;победил&quot;. **Оценивается несколько критериев** , такие как количество населения, качество жизни, общий доход.

1. Будет хранится локальный leaderboard. _Если Никита прям сильно захочет, то сможет сделать online leaderboard (через REST API или еще как-нибудь, хз, я это не шарю)_
2. Также можно будет сделать общий подсчет очков, и придумать формулу, типа: FinalScore = Population \* QualityOfLife + Money

**Таким образом, игра будет отличаться от типичного симулятора:**

В SimCity игра не пошаговая (то есть игрок не может отвлекаться и обязан за всем следить), игра длиться вечно (пока не надоест), и вообще, SimCity рассчитан на задротов. _А у нас игра будет упрощенная настолько, что можно будет даже разработать ее как Android-игру(???)_

**А как именно выглядит геймплей?**

**Если не учитывать эти особенности** , то игра во многом будет похожа на SimCity. Советую посмотреть какой-нибудь летсплей, или самим поиграть, чтобы понять, о чем речь.

**Три вида основных зданий** : промышленность, спальный район, магазины. Это стандартная схема во всех Симситях, ничего сверх-нового.

Все эти здания делятся на несколько классов: **низшие, средние и богатые**. Богатые люди очень требовательные, но зато платят много налогов.

Также у нас будут особенные здания: полицейский участок, больница, пожарные, школа, университет, парк и т.д.

**Вопрос: что из этого моделировать, а что - нет? Это надо обсудить.**

В SimCity симулируется уровень преступности, пожары, болезни, уровень образования… Я предлагаю в нашей игре не моделировать все эти вещи, а сделать один общий параметр: Quality of Life(™). Например, если рядом нет больниц, то Quality of Life снижается, и всё.

Еще одна важная часть симулятора, которую стоит понимать: **симуляция строится на основе системы спроса и предложения (Supply &amp; Demand).** Эта система затрагивает три основных вида зданий, и три класса, то есть всего 9 разных &quot;категорий&quot;. Не знаю, как это нормально обьяснить, поэтому примеры:

1. Если Quality of Life очень высокий, в городе есть университеты, парки, и т.д. то туда захотят приехать богатые люди. Они захотят себе роскошные дома. Поэтому **повышается спрос на высококлассное жильё.**
2. Следующий ход: игрок строит высококлассное жилье, приезжают мажоры, заселяют дома, всё такое. Но теперь эти люди хотят себе дорогие магазины, в итоге **повышается спрос на высококлассные магазины.**
3. В то же время, эти люди занимают все крутые рабочие места, соответственно **спрос на жилье для богатых падает** (так как найти себе достойную работу становится труднее).
4. Если город слишком мажорный, то бедные люди не смогут позволить себе там жить, в итоге **спрос на бедные дома** падает.
5. В то же время, город не может состоять из 100% богатых людей, так как тогда некому будет работать в школах, пожарных станциях, в магазинах, и т.д. Так что всегда будет **спрос на бедные дома.**
6. И т.д.

Игроку будет показываться уровень спроса для всех категорий, чтобы он мог делать осознанный выбор.

Балансировать это всё будет нелегко, но нам необязательно делать сбалансированную игру, главное: показать Жеребу.

_(а потом летом доделаем, выложим в Стим и станем миллионерами, ага)_

Если это слишком сложно/слишком много всего, то кидайте идеи, как это упростить.

Разработка геймплея:

**Предыстория:**

Вы известный градостроитель, который облагородил множество городов от Сан Франциско до Кентукки. Однако у вас есть один небольшой изъян: вы очень любите спать. Прям ооочень. Раз в год вы просыпаетесь на 1 день.

Поэтому, у вас есть только 1 день для того, чтоб спланировать развитие города на 1 год. Вас наняли для помощи одному очень необычному городу: \&lt;Ваш город\&gt;. Сможете ли вы стать той самой надеждой этого города?

**Виды зданий:**

- Factory
- House
- Shop
- Road(связывание этих обьектов)

**Виды природных обьектов:**

- Равнина
- Гора
- Река

Можно сделать, что для построения каждого нового здания одного вида нужно больше денег.

При построение каждого здания его вид будет рандомным(Factory1.png, Factory2.png,...)

Как это будет выглядеть. У нас есть карта

![](https://github.com/Nikitosis/OOP_Game/blob/master/media/preview/Simple.png)

На ней находятся разные здания и обьекты.

Также в верхней левой части меню мы видем кол-во денег(и его прирост), качество экологии(и его прирост). В верхней правой части меню - название города, настроение граждан, популяция(и ее прирост).

В верхней левой части также видим кнопку следующего хода.

Мы выбираем клетку(кликаем на нее) и открывается информация о клетке:

![](https://github.com/Nikitosis/OOP_Game/blob/master/media/preview/Select%20grass.png)

Также эта клетка выделяется(обводиться и приподнимается). Здесь мы видим информацию о клетке, что находиться на данной клетке(grass), характеристики этой клетки(прирост популяции, денег, настроения и экологии). Также кнопку строения(синий план).

При нажатии на кнопку строения, открывается магазин:

![](https://github.com/Nikitosis/OOP_Game/blob/master/media/preview/Open%20shop.png)

Сдесь мы можем выбрать нужное нам строение. Заметим, что фон размывается для концентрации внимания игрока на магазине.

При покупке, клетка с травой меняется на клетку с Заводом:

![](https://github.com/Nikitosis/OOP_Game/blob/master/media/preview/Buy%20factory.png)

В клетках со строением появляется возможность ее сносить. При сносе баланс денег увеличивается, а клетка становиться клеткой с травой.
