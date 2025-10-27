**Лабораторна-практична робота №3**

**Тема:** Розробка та тестування захищеного REST API на Node.js та Express.

**Мета:** закріплення теоретичних знань та набуття практичних навичок з розробки, захисту та тестування серверних додатків на базі REST архітектури.

Знати:

- Принципи побудови RESTful API: робота з ресурсами, використання HTTP-методів та коректна обробка статусів відповіді.
- Фундаментальну різницю між процесами аутентифікації та авторизації.
- Роль та механізм роботи проміжних обробників (middleware) у фреймворку Express для реалізації наскрізної функціональності.
- Основні підходи до логування подій на сервері.

Вміти:

- Створювати та налаштовувати вебсервер за допомогою Node.js та Express.
- Розробляти API ендпоінти для управління ресурсами.
- Реалізовувати власні проміжні обробники (middleware) для впровадження механізмів аутентифікації, авторизації за ролями та логування.
- Тестувати розроблене API за допомогою різних клієнтських інструментів (Postman, Node.js скрипт).
- Вести розробку проєкту з використанням системи контролю версій Git та платформи GitHub.

**Хід роботи:**

***1. Підготовка проєкту та середовища***

**Створення репозиторію на `GitHub`**

Створюємо публічний репозиторій на GitHub з назвою `secure-api-lab`, вибираємо опцію `«Add .gitignore»` та у шаблонах обираємо `«Node»`, клонуємо його локально

Копіювання репозиторію та перехід у теку проєкту

Відкриваємо термінал (або `Git Bash` на `Windows`) і виконуємо наступні команди, підставивши `URL` свого репозиторію:

```bash
git **clone** <https://github.com/gn4r4/secure-api-lab>
```

**Ініціалізація `Node.js` проєкту.**

Переходимо до теки `secure-api-lab` за допомогою команди:

```bash
cd secure-api-lab
```

Ініціалізовуємо проєкт за допомогою менеджера пакетів `npm` (ця команда автоматично створить файл `package.json`):

```bash
npm init -y
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/1.png?raw=true)

Робимо коміт:

```bash
git add .
git commit -m "added package.json"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/2.png?raw=true)

**Вставновлення `Express`.**

Додаємо у наш проєкт фреймворк `Express` (він буде основою нашого сервера):

```bash
npm install express
```
>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/3.png?raw=true)

Після виконання цієї команди у нас зв'язилась директорія `node_modules` та файл `package-lock.json`

Робимо коміт:

```bash
git add .
git commit -m "installed express"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/4.png?raw=true)

**Створення базового вебсервера.**

Створюємо у кореневій теці проєкту файл `server.js` та додаємо до нього зазначений код

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/5.png?raw=true)

**Перевірка роботи сервера**

Запускаємо сервер командою в терміналі:

```bash
node server.js
```

Отримуємо у консолі повідомлення, що сервер запущений

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/6.png?raw=true)

Відкриваємо браузер, переходимо за посиланням <http://localhost:3000>

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/7.png?raw=true)

**Збереження результатів у `Git`.**

Зберігаємо результати першого етапу, зробивши коміт та відправивши зміни на `GitHub`

```bash
git add .
git commit -m "added server"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/8.png?raw=true)

***2. Реалізація базового `API` та даних***

**Створення файлу з даними.**

Створюємо окремий файл `data.js` для зберігання наших даних у корені нашого проєкту, додаємо до нього наступний вміст:

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/9.png?raw=true)

**Модифікація файлу server.js.**

Тепер підключаємо наші дані до основного файлу сервера та додаємо необхідний `middleware` для роботи з `JSON`

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/10.png?raw=true)

**Перевірка роботи ендпоінтів за допомогою `Postman`**

Перезапускаємо наш сервер:

```bash 
node server.js
```


Відкриваємо `Postman` і перевіряємо наступні запити:

- **GET <http://localhost:3000/documents>**: У відповідь ми повинні отримати `JSON-масив` із двома документами та статус **200 OK.**

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/11.png?raw=true)

- **GET <http://localhost:3000/employees>**: У відповідь ми повинні отримати `JSON-масив` із двома співробітниками та статус **200 OK.**

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/12.png?raw=true)

- **POST <http://localhost:3000/documents>**:
  - Встановіть метод запиту на **POST**.
  - Перейдіть на вкладку **Body**, виберіть режим **raw** та тип **JSON**.
  - Вставте у тіло запиту наступний `JSON`:

```bash
{  
  "title": "Q3 Financial Report",  
  "content": "The financial results for Q3 are positive."  
}
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/13.png?raw=true)

-   - Надсилаємо запит. У відповідь ми повинні отримати статус `201 Created` та `JSON-об'єкт` нашого нового документа з доданим полем `id`.
    - Робимо ще раз `GET` запит на `/documents`, щоб переконатись, що новий документ додався до списку

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/14.png?raw=true)

**Збереження результатів у `Git`.**

Робимо коміт

```bash
git add .
git commit -m "feat: Implement basic API endpoints and in-memory data"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/15.png?raw=true)

***3. Реалізація безпеки (`Аутентифікація` та `Авторизація`)***

Створюємо `Middleware` для аутентифікації (`authMiddleware`).

Ця функція буде щоб перевіряти, чи надав користувач коректі `логін` та `пароль` у заголовках запиту.

Додаємо наступний код у файл `server.js` перед розділом з маршрутами. Імпортуємо масив users з файлу `data.js`:

```bash
// server.js  
// ... ваш існуючий код (require, app, PORT, app.use(express.json()))  
// Імпортуємо всі дані, включаючи користувачів  
<br/>**const** { users, documents, employees } = require('./data');  
<br/>// --- MIDDLEWARE ---  
**const** authMiddleware = (req, res, next) => {  
  // Отримуємо дані для входу з заголовків запиту  
  **const** login = req.headers\['x-login'\];  
  **const** password = req.headers\['x-password'\];  
  // Шукаємо користувача у нашій "базі даних"  
<br/>  **const** user = users.find(u => u.login === login && u.password === password);  
<br/>  // Якщо користувача не знайдено, або дані невірні  
  **if** (!user) {  
    // Відповідаємо статусом 401 Unauthorized і припиняємо обробку  
    **return** res.status(401).json({ message: 'Authentication failed. Please provide valid credentials in headers X-Login and X-Password.' });  
  }  
<br/>  // Якщо користувач знайдений, додаємо його дані до об'єкта запиту  
  // Це дозволить наступним обробникам знати, хто надіслав запит  
<br/>  req.user = user;  
<br/>  // Передаємо управління наступному middleware або основному обробнику маршруту  
  next();  
};  
<br/>// --- КІНЕЦЬ MIDDLEWARE ---  
// --- МАРШРУТИ ДЛЯ РЕСУРСІВ ---
```

**Створення `Middleware` для авторизації.**

Ця функція буде перевіряти, чи має аутентифікований користувач роль `'admin'`. Додаємо цей код одразу після `authMiddleware`:

```bash
// server.js (продовження)  
<br/>**const** adminOnlyMiddleware = (req, res, next) => {  
<br/>  // Перевіряємо, чи існує об'єкт user і яка в нього роль  
  // req.user був доданий на попередньому етапі в authMiddleware  
<br/>  **if** (!req.user || req.user.role !== 'admin') {  
    // Якщо роль не 'admin', відповідаємо статусом 403 Forbidden  
    **return** res.status(403).json({ message: 'Access denied. Admin role required.' });  
<br/>  }  
<br/>  // Якщо перевірка пройдена, передаємо управління далі  
  next();  
};
```

**Застосування `Middleware` до маршрутів.**

Тепер «вбудовуємо» наші перевірки у ланцюжок обробки запитів для кожного маршруту. `Middleware` передаються як аргументи до функція `app.get()`, `app.post()` тощо, перед основним обробників.

Оновлюємо наші маршрути наступним чином:

```bash
// server.js (продовження)  
<br/>// --- МАРШРУТИ ДЛЯ РЕСУРСІВ ---  
<br/>// Всі запити до /documents вимагають лише аутентифікації  
app.get('/documents', authMiddleware, (req, res) => {  
  res.status(200).json(documents);  
});  
<br/>app.post('/documents', authMiddleware, (req, res) => {  
  **const** newDocument = req.body;  
  newDocument.id = Date.now();  
  documents.push(newDocument);  
  res.status(201).json(newDocument);  
});  
<br/>// Запити до /employees вимагають і аутентифікації, і прав адміністратора  
// Зверніть увагу на порядок: спочатку auth, потім adminOnly  
<br/>app.get('/employees', authMiddleware, adminOnlyMiddleware, (req, res) => {  
  res.status(200).json(employees);  
});
```

**Тестування захищених ендпоінтів**

Перезапускаємо сервер:

```bash 
node server.js
```

Відкриваємо `Postman` і перевіряємо наступні сценарії:

- **Сценарій 1 (Немає доступу):**
  - Робимо `GET` запит на <http://localhost:3000/documents> **без заголовків**.
  - **Очікуваний результат:** `Статус 401 Unauthorized`.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/16.png?raw=true)

- **Сценарій 2 (Доступ для `user`):**
  - Зробіть `GET` запит на <http://localhost:3000/documents>.
  - Перейдіть на вкладку **Headers**.
  - Додайте два заголовки: `X-Login` зі значенням `user1` та `X-Password` зі значенням `password123`.
  - **Очікуваний результат:** `Статус 200 OK` та список документів.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/17.png?raw=true)

- **Сценарій 3 (Заборона доступу для `user`):**
  - Зробіть `GET` запит на <http://localhost:3000/employees>, використовуючи ті ж самі заголовки, що і в попередньому кроці (`user1`).
  - **Очікуваний результат:** `Статус 403 Forbidden`.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/18.png?raw=true)

- **Сценарій 4 (Доступ для `admin`):**
  - Зробіть GET запит на <http://localhost:3000/employees>.
  - Змініть значення заголовків на: `X-Login` -> `admin1`, `X-Password` -> `password123`.
- **Очікуваний результат:** `Статус 200 OK` та список співробітників.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/19.png?raw=true)

**Збереження результатів у `Git`.**

Робимо коміт:

```bash
git add .
git commit -m "feat: Implement authentication and authorization middleware"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/20.png?raw=true)

***4. Реалізація логування***

**Створення `Middleware` для логування (`logginMiddleware`)**

Ця функція буде максимально простою. Вона буде лише фіксувати дані про запит і передавати його далі по ланцюжку.

Додаємо наступний код у файл `server.js` разом з іншими нашими `middleware` (перел розділом з маршрутами)

```bash
// server.js (додайте цей код до секції MIDDLEWARE)  
<br/>**const** loggingMiddleware = (req, res, next) => {  
  // Отримуємо поточний час, HTTP метод та URL запиту  
  **const** timestamp = **new** Date().toISOString();  
  **const** method = req.method;  
  **const** url = req.url;  
<br/>  // Виводимо інформацію в консоль  
  console.log(\`\[\${timestamp}\] \${method} \${url}\`);  
<br/>  // ВАЖЛИВО: передаємо управління наступному middleware  
  // Якщо не викликати next(), обробка запиту "зависне" на цьому місці  
<br/>  next();  
};
```

**Глобальне застосування `Middleware`.**

На відміну від `authMiddleware` та `adminOnlyMiddleware`, які ми застосовували до конкретних маршрутів, логер має працювати для абсолютно всіх запитів. Для цього ми зареєструємо його глобально за допомогою `app.use()`.

Знаходимо у файлі `server.js` місце після `app.use(express.json())`; і перед першим маршрутом додаємо новий рядок:

```bash
// server.js  
// ...  
<br/>app.use(express.json());  
<br/>// Глобально застосовуємо middleware для логування  
// Цей рядок має бути ПЕРЕД усіма маршрутами  
<br/>app.use(loggingMiddleware);  
<br/>// --- MIDDLEWARE ---  
**const** authMiddleware = (req, res, next) => { ... };  
**const** adminOnlyMiddleware = (req, res, next) => { ... };  
<br/>// --- МАРШРУТИ ДЛЯ РЕСУРСІВ ---  
// ...
```

**Перевірка роботи логера**

- Перезапускаємо наш сервер (`node server.js`).
- Відкриваємо `Postman` і надсилаємо будь-які 2-3 запити, які ми тестували на попередньому етапі (наприклад, успішний `GET /documents` та невдалий `GET /employees`).
- Дивимось на **консоль, де запущено наш сервер**.
- **Очікуваний результат:** Для кожного запиту, надісланого з `Postman`, у нашій консолі має з'явитись новий рядок логу.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/21.png?raw=true)

Це підтверджує, що наш `middleware` для логування успішно перехоплює та реєструє всі вхідні запити.

**Збереження результатів у Git**

Робимо коміт:

```bash
git add .
git commit -m "feat: Implement request logging middleware"
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/22.png?raw=true)

***5. Комплексе тестування***

**Доопрацювання сервера для повноцінного тестування**

Перед початком тестування нам потрібно трохи розширити функціонал сервера, щоб він міг обробляти всі необхідні сценарії та повертати відповідні статуси. Ми додамо валідацію для `POST-запитів` та можливість видаляти документи.

Оновлюємо наш маршрут `POST /documents` та додаємо новий маршрут `DELETE /documents/:id` у файл `server.js`:

```bash
// ... (в файлі server.js)  
<br/>// Оновлений маршрут для створення нового документа  
app.post('/documents', authMiddleware, (req, res) => {  
  **const** { title, content } = req.body;  
<br/>  // Перевірка, чи передані всі необхідні поля  
<br/>  **if** (!title || !content) {  
    **return** res.status(400).json({ message: 'Bad Request. Fields "title" and "content" are required.' });  
  }  
<br/>  **const** newDocument = {  
    id: Date.now(),  
    title,  
    content,  
  };  
<br/>  documents.push(newDocument);  
  res.status(201).json(newDocument);  
});  
<br/>// Новий маршрут для видалення документа за id  
<br/>app.delete('/documents/:id', authMiddleware, (req, res) => {  
    // Отримуємо id з параметрів маршруту  
    **const** documentId = parseInt(req.params.id);  
    **const** documentIndex = documents.findIndex(doc => doc.id === documentId);  
<br/>    // Якщо документ з таким id не знайдено  
    **if** (documentIndex === -1) {  
        **return** res.status(404).json({ message: 'Document not found' });  
    }  
<br/>    // Видаляємо документ з масиву  
    documents.splice(documentIndex, 1);  
<br/>    // Відповідаємо статусом 204 No Content, тіло відповіді буде порожнім  
    res.status(204).send();  
});  
<br/>// ... (решта маршрутів)
```

Після внесення змін перезапускаємо наш сервер:

```bash 
node server.js
```

**Проведення тестів**

Тепер, коли сервер готовий, перевіряємо його роботу трьома різними методами

**Тестування з рядка браузера**

- **Завдання:** Відкриваємо браузер і переходимо за адресою <http://localhost:3000/documents>.
- **Очікуваний результат:** Сторінка повинна відображати помилку (наприклад, {"message":"Authentication failed..."}).
- **Аналіз:** Вікдриваємо інструменти розробника (`F12`), переходимо на вкладку `"Network"`. Бачите, що сервер повернув статус 401 Unauthorized, тому що браузер не надсилає необхідні заголовки `X-Login` та `X-Password`.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/23.png?raw=true)

**Тестування за допомогою Postman.**

Створюємо у `Postman` колекцію запитів для перевірки всіх можливих сценаріїв

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `GET` | `/documents` | \-  | \-  | **401 Unauthorized** | Спроба доступу без аутентифікації. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/24.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `GET` | `/employees` | `X-Login`: `user1`<br><br>`X-Password`: `password123` | \-  | **403 Forbidden** | Спроба доступу до адмін-ресурсу з роллю 'user'. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/25.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `GET` | `/documents` | `X-Login`: `user1`<br><br>`X-Password`: `password123` | \-  | **200 OK** | Успішне отримання даних з роллю 'user'. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/26.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `GET` | `/employees` | `X-Login`: `admin1`<br><br>`X-Password`: `password123` | \-  | **200 OK** | Успішне отримання даних з роллю 'admin'. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/27.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `POST` | `/documents` | `X-Login`: `user1`<br><br>`X-Password`: `password123` | { "title": "Test Doc", "content": "..." } | **201 Created** | Успішне створення ресурсу. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/28.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `POST` | `/documents` | `X-Login`: `user1`<br><br>`X-Password`: `password123` | { "content": "..." } | **400 Bad Request** | Помилка валідації (відсутнє поле title). |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/29.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `DELETE` | `/documents/1` | `X-Login`: `admin1`<br><br>`X-Password`: `password123` | \-  | **204 No Content** | Успішне видалення. Відповідь не має тіла. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/30.png?raw=true)

| **Метод** | **URL** | **Заголовки (Headers)** | **Тіло (Body)** | **Очікуваний статус** | **Примітка** |
| --- | --- | --- | --- | --- | --- |
| `GET` | `/non-existent` | `X-Login`: `admin1`<br><br>`X-Password`: `password123` | \-  | **404 Not Found** | Звернення до неіснуючого маршруту. |

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/31.png?raw=true)

**Тестування за допомогою `Node.js` скрипта**

Створюємо у проєкті новий файл `test-client.js`:

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/32.png?raw=true)

Відкриваємо новий термінал (не закриваючи, де працює сервер) і виконуємо команду node `test-client.js`. Аналізуємо вивід у консолі.

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/33.png?raw=true)

Робимо коміт:

```bash
git add .  
git commit -m "feat: Complete final testing of the API"  
git push origin main
```

>![placeholder](https://github.com/gn4r4/secure-api-lab/blob/main/images/34.png?raw=true)
