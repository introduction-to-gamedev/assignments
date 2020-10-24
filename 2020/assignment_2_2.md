###### Практична робота №2.2
## Змагання зі штучного інтелекту для Антиреверсі

### Мета роботи:
Зануритись трохи більше в тему штучного інтелекту для дискретних ігор та визначити всередині потоку яка команда - чемпіон

### Деталі
Всі створені в роботі 2.1 боти для гри в антіреверсі працюють через спільний інтерфейс командної строки, а це означає що вони можуть грати не тільки з тестером, що робить випадкові ходи, а і один із одним. В межах цієї роботи ми проведемо чемпіонат в декілька турів, який дозволить обрати найкращого бота. Команди-призери отримують бонус до рейтингу та викарбують свої імена в історії.

### Як все буде проходити? 
Змагання буде складатися з декількох турів, в кожному турі допущені боти бути грати чемпіонат по системі "кожен з кожним". Кожна дуель між двома ботами буде складатися з серії матчів, поки один з ботів не набере 5 очок (перемога - 1 очко, нічия - по 0.5 кожній стороні, поразка - 0). За підсумками всіх ігор буде складено турнірна таблиця, де перші 8 команд отримують залікові очки за раунд.

Логи всіх ігор раунду будуть викладені у відкритий доступ для аналізу, перед кожним наступним раундом команди матимуть змогу зробити апдейт власного клієнту.

Розклад змагання:

|Дата|Номер раунду|Залікові очки|
|:----------:|:--:|-------------|
|1 листопада |0|не нараховуються*|
|15 листопада|1|10-8-6-5-4-3-2-1|
|29 листопада|2|х2 до очок першого раунду|
|13 грудня|3|х3 до очок першого раунду|

 *- До нульового раунду будуть допущені всі команди, що встигли вкластися в soft deadline. Турнірна таблиця буде складена, але очки не нараховуються - в цьому раунді команди зможуть оцінити крутість свого бота порівняно інших. Команди, що не вкладуться в софт-дедлайн такої можливості не матимуть.

Зверніть увагу, вартість і цінність кожного наступного раунду росте через запас часу для вдосконалення ботів.

### І як написати найкращого бота?
В межах заданих лімітів по оперативній пам'яті та часу обмежень по алгоритмам немає. Цілком можливо, що для перемоги буде достатньо продумати гарну SEV та прокачати мінімакс до його просунутих варіацій (наприклад, Negascoutу). Можна спробувати замахнутись на Monte-Carlo Search Tree чи ML, або пошукати щось більш екзотичне.

### Які призи?
- 1 місце: +7 балів до рейтингу та спеціальний приз ;)
- 2 місце: +5 балів до рейтингу
- 3 місце: +3 бали до рейтингу