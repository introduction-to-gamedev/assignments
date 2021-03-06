###### Практична робота №2.1
## Розробка штучного інтелекту для варіації гри Reversi

### Мета роботи:
Розібратися з алгоритмами штучного інтелекту, що використовуються для детермінованих ігор з повною інформацією. Реалізувати штучний інтелект для однієї з варіацій гри реверсі. 

### Завдання:
В минулій роботи було реалізовано клієнт для гри реверсі. Як ви пам'ятаєте, окремим пунктом в завданнях було вказано звернути увагу на розділення коду на модулі - модель, обробку введення та візуалізацію. В данній роботі нам знадобиться зроблена модель (input та view доведеться створити нові), оскільки ціль роботи - створення штучного інтелекту для гри.

Практична робота №2 складається з двох частин:
1. Створити штучний інтелект, що буде перемагати опонента який ходить випадковими ходами у 90% (або більше) випадків. Виконання цього пункту дозволить отримати базову кількість балів. В цьому документі описана саме ця частина.
2. Створити бота, що буде здатен перемогти ботів інших команд. Змагання буде проходити в декілька турів, команди що будуть проходити в кожен наступний тур будуть отримувати додаткові бали.


### Деталі
Перший важливий момент - гра в реверсі достатньо добре вивчена на предмет штучного інтелекту, тому, для того щоб зробити процес написання АІ більш цікавим та творчим, ми будемо грати не в реверсі, а в варіацію цієї гри - **антіреверсі з чорною дірою**. Антіреверсі означає що ціллю гравця наприкінці гри є отримання не більшої кількості фішок на полі, а меншої. Зверніть увагу - для того щоб перемогти у антіреверсі недостатньо просто погано грати у реверсі, ця гра має власну стратегію. Чорна діра означає що в кожній партії випадковим чином обирається одна клітинка на полі, на яку не можна ставити фішки.

За умовами завдання не виставляється конкретна вимога який саме алгоритм реалізовувати для штучного інтелекту, проте я рекомендую почати з мінімаксу: реалізувати власне дерево мінімаксу, подумати про підрахунок SEV, далі додати альфа\бета відсікання для збільшення глибини прорахунку та ускладнювати бота лише ітеративно. Рекомендую братися за більш складні варіанти (наприклад, MCTS) тільки коли ви будете мати робочу версію з мінімаксом, яка проходить всі тести.

Другий - Для того щоб мати змогу змагатися один з одним, боти мають реалізовувати певний спільний інтерфейс. Найпростішим варіантом такого інтерфейсу є командний рядок, оскільки створити подібну програму можна за допомогою всіх розповсюджених мов програмування та платформ. Отже, якщо попередня робота виконана вами коректно, то вам не буде складно підмінити введення з графічного (з клієнту) на введення з командної строки, а виведення ходу - на вивід в командний рядок.

Вимоги до програми:
1. Програма має запускатися через командний рядок та зчитувати ввід з system.in
2. На початку виконання программа отримає на ввід строку з координатами чорної діри (наприклад, `А3`)
3. Другою командою прийде строка з вказанням кольору, яким пропонується грати (у форматі `white` або `black`). Чорні ходять першими, тому якщо чорними грає ваш бот, одразу після другої команди будуть на очікуватися координати ходу. Якщо білими - третьою командою прийде хід чорних
4. Далі програма має видавати наступний хід після кожного введенего ходу противника або ключове слово pass у разі відсутності ходів

Программа буде тестуватися за допомогою спеціального клієнта, який буде її запускати та виступати в ролі противника, що ходить випадковими ходами. Вихідний код тестувальника буде викладено незабаром. Для того щоб тест був пройдений успішно, команда отримала базові бали та була допущена до змагання (робота 2.2), необхідно щоб виконувалися наступні умови:
1. При запускові 100 раундів ігор проти бота, бот перемагає у 90 або більше.
2. Бот працює без помилок: будь-яка помилка у рантаймі програми буде призводити до зарахування технічної поразки в раунді.
3. Бот працює у рамках виділених ресурсів: кожен хід вкладається у 2 секунди, бот використовує не більше 1Гб оперативної пам'яті. Вихід за рамки цих вимог також призводить до технічної поразки. Обмеження у 2 секунди буде вимірюватися на тестовому пристрої з CPU i7-8700.
4. Технічна поразка також зараховується у випадку якщо програма видає неможливий на даний момент хід.
 
Розглянемо приклад командної строки при роботі з ботом (`->` - ввід, `<-` - вивід з програми):

```
-> B3    //перша команда - координати чорної діри
-> black //друга - колір
<- C5    //бот грає чорними, тому виводить свій хід
-> C4    //на вхід подається наступний хід опонента
```
і так далі

Схема розмітки поля та стартова позиція:

![reversi field](https://github.com/introduction-to-gamedev/assignments/blob/master/res/reversi-start.png "Стартова позиція")

Перед здачею роботи необхідно зібрати консольний додаток під win64 додати у релізи на вашому гітхаб-репозиторії

### Оцінювання:
- бот перемагає у 90 іграх зі 100 - *4 бали*
- бот перемагає у 100 іграх зі 100 - *1 бал*
- бот не отримує жодної технічної поразки - *1 бал*
- якість написання коду - *2 бали*

### Матеріали:
- [Лекція із штучного інтелекту (minimax, MCST)](https://www.youtube.com/watch?v=zlEI6ii28_A&list=PLkgXLMuasx7C7yMUsaq366htPg9rpM2lw&index=5)
- [Стаття з мінімаксу на вікіпедії](https://en.wikipedia.org/wiki/Minimax)
- [Альфа\бета відсікання](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning)

### Література
Посилання йдуть амазон, але всі матеріали можна знайти в мережі
- [AI for games (chapter 9)](https://www.amazon.com/AI-Games-Third-Ian-Millington/dp/1138483974)
