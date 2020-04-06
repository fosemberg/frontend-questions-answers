## Вопросы и ответы по js

**JavaScript**:

<details>
<summary>Какие типы данных существуют в JavaScript?</summary>
<div>
  <ul>
    <li>
      Число <b>«number»</b> - Единый тип число используется как для целых, так и для дробных чисел. Существуют специальные числовые значения Infinity (бесконечность) и NaN (ошибка вычислений). Например, бесконечность Infinity получается при делении на ноль. Ошибка вычислений NaN будет результатом некорректной математической операции.
    </li>
    <li>
      Строка <b>«string»</b>
    </li>
    <li>
      Булевый (логический) тип <b>«boolean»</b>
    </li>
    <li>
      Специальное значение <b>«null»</b> - В JavaScript null не является «ссылкой на несуществующий объект» или «нулевым указателем», как в некоторых других языках. Это просто специальное значение, которое имеет смысл «ничего» или «значение неизвестно».
    </li>
    <li>
       Специальное значение <b>«undefined»</b> - Значение undefined, как и null, образует свой собственный тип, состоящий из одного этого значения. Оно имеет смысл «значение не присвоено». Если переменная объявлена, но в неё ничего не записано, то её значение как раз и есть undefined.
    </li>
    <li>
      Объекты <b>«object»</b> - Первые 5 типов называют «примитивными». Особняком стоит шестой тип: «объекты». Он используется для коллекций данных и для объявления более сложных сущностей. Объявляются объекты при помощи фигурных скобок {...}
    </li>
  </ul>
  <p><i>Источник: <a href ="https://learn.javascript.ru/types-intro">learn.javascript.ru</a></i></p>
</div>
</details>

<details>
<summary>Что такое цикл событий (event loop) и как он работает?</summary>
<div>
  <p>Движок браузера выполняет JavaScript в одном потоке. Для потока выделяется область памяти — стэк, где хранятся фреймы (аргументы, локальные переменные) вызываемых функций.</p>
  <p>Список событий, подлежащих обработке формируют очередь событий. Когда стек освобождается, движок может обрабатывать событие из очереди. Координирование этого процесса и происходит в event loop.</p>
  <p>Это по сути бесконечный цикл, в котором выполняются многочисленные обработчики событий. Если очередь пустая — движок браузера ждет, когда поступит событие. Если непустая — первое в ней событие извлекается и его обработчик начинает выполняться. И так до бесконечности.</p>
   <img src="https://cdn-images-1.medium.com/max/1600/1*quyTIOs2hioCx1jRQ7-ojw.png" />
   <p><i>Источник: <a href ="https://medium.com/@pavelbely/javascript-event-loop-%D0%B2-%D0%BA%D0%B0%D1%80%D1%82%D0%B8%D0%BD%D0%BA%D0%B0%D1%85-%D1%87%D0%B0%D1%81%D1%82%D1%8C-1-a19e4d99f242">Pavel Bely, medium.com</a></i></p>
</div>
</details>

<details>
<summary>Что такое замыкание?</summary>
<div>
  <p>Замыкание — это комбинация функции и лексического окружения, в котором эта функция была объявлена. Это окружение состоит из произвольного количества локальных переменных, которые были в области действия функции во время создания замыкания.</p>
  <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/JavaScript/Closures">developer.mozilla.org</a></i></p>
</div>
</details>

<details>
<summary>Что такое прототип объекта в JavaScript?</summary>
<div>
  <p>Объекты в JavaScript можно организовать в цепочки так, чтобы свойство, не найденное в одном объекте, автоматически искалось бы в другом. Связующим звеном выступает специальное свойство __proto__</p>
  <p>Если один объект имеет специальную ссылку __proto__ на другой объект, то при чтении свойства из него, если свойство отсутствует в самом объекте, оно ищется в объекте __proto__. Недостаток этого подхода – он не работает в IE10-.</p>
  <p>К счастью, в JavaScript с древнейших времён существует альтернативный, встроенный в язык и полностью кросс-браузерный способ. Чтобы новым объектам автоматически ставить прототип, конструктору ставится свойство prototype.</p>
  <p>При создании объекта через new, в его прототип __proto__ записывается ссылка из prototype функции-конструктора.</p>
  <p>Значением Person.prototype по умолчанию является объект с единственным свойством constructor, содержащим ссылку на Person.</p>
  <p><i>Источник: <a href ="https://learn.javascript.ru/prototype">learn.javascript.ru</a></i></p>
</div>
</details>

<details>
<summary>Как работает ключевое слово this?</summary>
<div>
  <p>В глобальном контексте выполнения (за пределами каких-либо функций), this ссылается на глобальный объект вне зависимости от использования в строгом или нестрогом режиме.</p>
  <p>В пределах функции значение this зависит от того, каким образом вызвана функция:</p>
  <ul>
  <li>Простой вызов - В этом случае значение this не устанавливается вызовом. Так как этот код написан не в строгом режиме, значением this всегда должен быть объект, по умолчанию - глобальный объект. В строгом режиме, значение this остается тем значением, которое было установлено в контексте исполнения. Если такое значение не определено, оно остается undefined. Для того что бы передать значение this от одного контекста другому необходимо использовать call или apply</li>
  <li>В стрелочных функциях, this привязан к окружению, в котором была создана функция. В глобальной области видимости, this будет указывать на глобальный объект. </li>
  <li>Когда функция вызывается как метод объекта, используемое в этой функции ключевое слово this принимает значение объекта, по отношению к которому вызван метод.</li>
  </ul>
  <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/this">developer.mozilla.org</a></i></p>
</div>
</details>

<details>
<summary>Как работают методы apply(), call() и bind()?</summary>
<div>
  <p>Функции в JavaScript никак не привязаны к своему контексту this, с одной стороны, здорово – это позволяет быть максимально гибкими, одалживать методы и так далее.</p>
  <p>Но с другой стороны – в некоторых случаях контекст может быть потерян. Способы явно указать this  - методоы bind, call и apply.</p>
  <ul>
    <li>
      <p>Синтаксис метода call: func.call(context, arg1, arg2, ...)</p>
      <p>При этом вызывается функция func, первый аргумент call становится её this, а остальные передаются «как есть». Вызов func.call(context, a, b...) – то же, что обычный вызов func(a, b...), но с явно указанным this(=context).</p>
    </li>
    <li>
      <p>Если нам неизвестно, с каким количеством аргументов понадобится вызвать функцию, можно использовать более мощный метод: apply. Вызов функции при помощи func.apply работает аналогично func.call, но принимает массив аргументов вместо списка.</p>
      <p>
        func.call(context, arg1, arg2) идентичен вызову func.apply(context, [arg1, arg2]);
      </p>
    </li>
    <li>
      <p>Синтаксис встроенного bind: var wrapper = func.bind(context[, arg1, arg2...])</p>
      <p>Методы bind и call/apply близки по синтаксису, но есть важнейшее отличие. Методы call/apply вызывают функцию с заданным контекстом и аргументами. А bind не вызывает функцию. Он только возвращает «обёртку», которую мы можем вызвать позже, и которая передаст вызов в исходную функцию, с привязанным контекстом.</p>
    </li>
  </ul>
  <p>
    <i>Источник:
      <br/>
      <a href ="https://learn.javascript.ru/call-apply#metod-apply">javascript.ru - call и apply</a>
      <br/>
      <a href ="https://learn.javascript.ru/bind#bind">javascript.ru - bind</a>
    </i>
  </p>
</div>
</details>

<details>
<summary>Что такое Promise (Промис)?</summary>
<div>
  <br/>
  <p>Promise – это специальный объект, который содержит своё состояние. Вначале pending («ожидание»), затем – одно из: fulfilled («выполнено успешно») или rejected («выполнено с ошибкой»).</p>
  <p>
    Синтаксис создания Promise:

    var promise = new Promise(function(resolve, reject) {
      // Эта функция будет вызвана автоматически

      // В ней можно делать любые асинхронные операции,
      // А когда они завершатся — нужно вызвать одно из:
      // resolve(результат) при успешном выполнении
      // reject(ошибка) при ошибке
    })
  </p>
  <p>
    Универсальный метод для навешивания обработчиков:
    
    promise.then(onFulfilled, onRejected)
    
  <ul>
    <li>onFulfilled – функция, которая будет вызвана с результатом при resolve.</li>
    <li>onRejected – функция, которая будет вызвана с ошибкой при reject.</li>
  </ul>
    Для того, чтобы поставить обработчик только на ошибку, вместо .then(null, onRejected) можно написать .catch(onRejected) – это то же самое.
  </p>
  <p>
    Возьмём setTimeout в качестве асинхронной операции, которая должна через некоторое время успешно завершиться с результатом «result»:
  
    // Создаётся объект promise
    let promise = new Promise((resolve, reject) => {

      setTimeout(() => {
        // переведёт промис в состояние fulfilled с результатом "result"
        resolve("result");
      }, 1000);

    });

    // promise.then навешивает обработчики на успешный результат или ошибку
    promise
      .then(
        result => {
          // первая функция-обработчик - запустится при вызове resolve
          alert("Fulfilled: " + result); // result - аргумент resolve
        },
        error => {
          // вторая функция - запустится при вызове reject
          alert("Rejected: " + error); // error - аргумент reject
        }
      );
   В результате запуска кода выше – через 1 секунду выведется «Fulfilled: result».
  </p>
  <p><i>Источник: <a href ="https://learn.javascript.ru/promise">javascript.ru</a></i></p>
</div>
</details>

**Веб - технологии**:

<details>
  <summary>Что такое HTTP?</summary>
  <div>
    <p>
      Протокол передачи гипертекста (Hypertext Transfer Protocol - HTTP) - это прикладной протокол для передачи гипертекстовых документов, таких как HTML. Он создан для связи между веб-браузерами и веб-серверами, хотя в принципе HTTP может использоваться и для других целей. Протокол следует классической клиент-серверной модели, когда клиент открывает соединение для создания запроса, а затем ждет ответа. HTTP - это протокол без сохранения состояния, то есть сервер не сохраняет никаких данных (состояние) между двумя парами "запрос-ответ". Несмотря на то, что HTTP основан на TCP/IP, он также может использовать любой другой протокол транспортного уровня с гарантированной доставкой.
    </p>
    <p>
      Ниже перечислены общие функции, управляемые с HTTP:
    </p>
    <ul>
      <li>
        <b>Кэш.</b> Сервер может инструктировать прокси и клиенты: что и как долго кэшировать. Клиент может инструктировать прокси промежуточных кэшей игнорировать хранимые документы.
      </li>
      <li>
        <b>Ослабление ограничений источника.</b> Для предотвращения шпионских и других, нарушающих приватность, вторжений, веб-браузер обчеспечивает строгое разделеление между веб-сайтами. Только страницы из того же источника могут получить доступ к информации на веб-странице. Хотя такие ограничение нагружают сервер, заголовки HTTP могут ослабить строгое разделение на стороне сервера, позволяя документу стать частью информации с различных доменов (по причинам безопасности).
      </li>
      <li>
        <b>Аутентификация.</b> Некоторые страницы доступны только специальным пользователям. Базовая аутентификация может предоставляться через HTTP, либо через использование заголовка WWW-Authenticate и подобных ему, либо с помощью настройки спецсессии, используя куки.
      </li>
      <li>
        <b>Прокси и тунелирование.</b> Серверы и/или клиенты часто располагаются в интранете, и скрывают свои истинные IP-адреса от других. HTTP запросы идут через прокси для пересечения этого сетевого барьера. Не все прокси -- HTTP прокси. SOCKS-протокол, например, оперирует на более низком уровне. Другие, как, например, ftp, могут быть обработаны этими прокси.
      </li>
      <li>
        <b>Сессии.</b> Использование HTTP кук позволяет связать запрос с состоянием на сервере. Это создает сессию,  хотя ядро HTTP -- протокол без состояния.  Это полезно не только для корзин в интернет-магазинах, но также для любых сайтов, позволяющих пользователю настроить выход.
      </li>
    </ul>
    <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/HTTP/Overview">developer.mozilla.org</a></i></p>
  </div>
</details>

<details>
  <summary>Из чего состоит HTTP-запрос?</summary>
  <div>
    <img src='https://mdn.mozillademos.org/files/13687/HTTP_Request.png' />
    <p>
      Запросы содержат следующие элементы:
    </p>
    <ul>
      <li>
        HTTP-метод, обычно глагол подобно GET, POST или существительное, как OPTIONS или HEAD, определяющее операцию, которую клиент хочет выполнить. Обычно, клиент хочет получить ресурс (используя GET) или передать значения HTML-формы (используя POST), хотя другие операция могут быть необходимы в других случаях.
      </li>
      <li>
        Путь к ресурсу: URL ресурсы лишены элементов, которые очевидны из контекста, например без protocol (http://), domain (здесь developer.mozilla.org), или TCP port (здесь 80).
      </li>
      <li>
        Версию HTTP-протокола.
      </li>
      <li>
        Заголовки  (опционально), предоставляюшие дополнительную информацию для сервера.
      </li>
      <li>
        Или тело, для некоторых методов, таких как POST, которое содержит отправленный ресурс.
      </li>
    </ul>
    <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/HTTP/Overview">developer.mozilla.org</a></i></p>
  </div>
</details>

<details>
  <summary>Какие методы может иметь HTTP-запрос?</summary>
  <div>
    <p>
      HTTP определяет множество методов запроса, которые указывают, какое желаемое действие выполнится для данного ресурса. Несмотря на то, что их названия могут быть существительными, эти методы запроса иногда называются HTTP глаголами. Каждый реализует свою семантику, но каждая группа команд разделяет общие свойства: так, методы могут быть безопасными, идемпотентными или кэшируемыми.
    </p>
    <ul>
      <li>
        <b>GET</b> запрашивает представление ресурса. Запросы с использованием этого метода могут только извлекать данные.
      </li>
      <li>
        <b>HEAD</b> запрашивает ресурс так же, как и метод GET, но без тела ответа.
      </li>
      <li>
        <b>POST</b> используется для отправки сущностей к определённому ресурсу. Часто вызывает изменение состояния или какие-то побочные эффекты на сервере.
      </li>
      <li>
        <b>PUT</b> заменяет все текущие представления ресурса данными запроса.
      </li>
      <li>
        <b>DELETE</b> удаляет указанный ресурс.
      </li>
      <li>
        <b>CONNECT</b> устанавливает "туннель" к серверу, определённому по ресурсу.
      </li>
      <li>
        <b>OPTIONS</b> используется для описания параметров соединения с ресурсом.
      </li>
      <li>
        <b>TRACE</b> выполняет вызов возвращаемого тестового сообщения с ресурса.
      </li>
      <li>
        <b>PATCH</b> используется для частичного изменения ресурса.
      </li>
    </ul>
    <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/HTTP/Methods">developer.mozilla.org</a></i></p>
  </div>
</details>

<details>
  <summary>Что такое Cross-Origin Resource Sharing (CORS)?</summary>
  <div>
    <p>
      Cross-Origin Resource Sharing (CORS) — механизм, использующий дополнительные HTTP-заголовки, чтобы дать возможность агенту пользователя получать разрешения на доступ к выбранным ресурсам с сервера на источнике (домене), отличном от того, что сайт использует в данный момент. Говорят, что агент пользователя делает запрос с другого источника (cross-origin HTTP request), если источник текущего документа отличается от запрашиваемого ресурса доменом, протоколом или портом.
    </p>
    <p>
      В целях безопасности браузеры ограничивают cross-origin запросы, инициируемые скриптами. Например, XMLHttpRequest и Fetch API следуют политике одного источника (same-origin policy). Это значит, что web-приложения, использующие такие API, могут запрашивать HTTP-ресурсы только с того домена, с которого были загружены, пока не будут использованы CORS-заголовки.
    </p>
    <p><i>Источник: <a href ="https://developer.mozilla.org/ru/docs/Web/HTTP/CORS">developer.mozilla.org</a></i></p>
  </div>
</details>

<details>
  <summary>Что такое HTTP cookie и для чего их используют?</summary>
  <div>
    <p>
      HTTP cookie (web cookie, cookie браузера) - это небольшой фрагмент данных, отправляемый сервером на браузер пользователя, который тот может сохранить и отсылать обратно с новым запросом к данному серверу. Это, в частности, позволяет узнать, с одного ли браузера пришли оба запроса (например, для аутентификации пользователя). Они запоминают информацию о состоянии для протокола HTTP, который сам по себе этого делать не умеет.
    </p>
    <p>
      Cookie используются, главным образом, для:
    </p>
    <ul>
      <li>
        Управления сеансом (логины, корзины для виртуальных покупок)
      </li>
      <li>
        Персонализации (пользовательские предпочтения)
      </li>
      <li>
        Мониторинга (отслеживания поведения пользователя)
      </li>
    </ul>
    <p>
      Получив HTTP-запрос, вместе с откликом сервер может отправить заголовок  Set-Cookie с ответом. Cookie обычно запоминаются браузером и посылаются в значении заголовка HTTP  Cookie с каждым новым запросом к одному и тому же серверу. Можно задать срок действия cookie, а также срок его жизни, после которого cookie не будет отправляться. Также можно указать  ограничения на путь и домен, то есть указать, в течении какого времени и к какому сайту  оно отсылается.
    </p>
    <p>
      Куки можно создавать через JavaScript при помощи свойства Document.cookie. Если флаг HttpOnly не установлен, то и доступ к существующим cookies можно получить через JavaScript.
    </p>

      document.cookie = "yummy_cookie=choco"; 
      document.cookie = "tasty_cookie=strawberry";
   <p><i>Источник: <a href="https://developer.mozilla.org/ru/docs/Web/HTTP/%D0%9A%D1%83%D0%BA%D0%B8">developer.mozilla.org</a></i></p>
  </div>
</details>

<details>
  <summary>Что такое Babel и для чего он используется?</summary>
  <div>
    <br/>
    <p>
      Babel.JS – это транспайлер, переписывающий код на ES-2015 в код на предыдущем стандарте ES5.
    </p>
    <p>
      Обычно Babel.JS работает на сервере в составе системы сборки JS-кода (например webpack или brunch) и автоматически переписывает весь код в ES5.
    </p>
    <p>
      Настройка такой конвертации тривиальна, единственно – нужно поднять саму систему сборки, а добавить к ней Babel легко, плагины есть к любой из них.
    </p>
    <p>
      Конфигурация Babel прописывается в файле babel.config.js, либо в .babelrc для настроек одного пакета, а также в package.json или .babelrc.js
    </p>
    <p>
    Пример конфига в babel.config.js:
      
      module.exports = function (api) {
        api.cache(true);

        const presets = [ ... ];
        const plugins = [ ... ];

        return {
          presets,
          plugins
        };
      }
   </p>
    <p>
     <i>
       Источник: 
        <a href="https://learn.javascript.ru/es-modern-usage#babel-js">learn.javascript.ru</a>, 
        <a href="https://babeljs.io/docs/en/next/configuration">babeljs.io</a>
     </i>
    </p>
  </div>
</details>

<details>
  <summary>Для чего используется WebSocket? В чем принцип его работы?</summary>
  <div>
    <br/>
    <p>
      Протокол WebSocket («веб-сокет»), описанный в спецификации RFC 6455, обеспечивает возможность обмена данными между браузером и сервером через постоянное соединение. Данные передаются по нему в обоих направлениях в виде «пакетов», без разрыва соединения и дополнительных HTTP-запросов.
    </p>
    <p>
      Чтобы открыть веб-сокет-соединение, нам нужно создать объект new WebSocket, указав в url-адресе специальный протокол ws:
      <code>
        let socket = new WebSocket("ws://javascript.info");
      </code>
    </p>
    <p>
      Как только объект WebSocket создан, мы должны слушать его события. Их всего 4:
    </p>
    <ul>
      <li>
        <b>open</b> – соединение установлено,
      </li>
      <li>
        <b>message</b> – получены данные,
      </li>
      <li>
        <b>error</b> – ошибка,
      </li>
      <li>
        <b>close</b> – соединение закрыто.
      </li>
    </ul>
    <p>
      Вот пример:
    </p>
    <p>
      
      let socket = new WebSocket("wss://javascript.info/article/websocket/demo/hello");
      
      socket.onopen = function(e) {
        alert("[open] Соединение установлено");
        alert("Отправляем данные на сервер");
        socket.send("Меня зовут Джон");
      };
      
      socket.onmessage = function(event) {
        alert(`[message] Данные получены с сервера: ${event.data}`);
      };
      
      socket.onclose = function(event) {
        if (event.wasClean) {
          alert(`[close] Соединение закрыто чисто, код=${event.code} причина=${event.reason}`);
        } else {
          // например, сервер убил процесс или сеть недоступна
          // обычно в этом случае event.code 1006
          alert('[close] Соединение прервано');
        }
      };
      
      socket.onerror = function(error) {
        alert(`[error] ${error.message}`);
      };
   </p>
    <p>
      Вызов socket.send(body) принимает body в виде строки или любом бинарном формате включая Blob, ArrayBuffer и другие. Дополнительных настроек не требуется, просто отправляем в любом формате. При получении данных, текст всегда поступает в виде строки. А для бинарных данных мы можем выбрать один из двух форматов: Blob или ArrayBuffer.
    </p>
    <p>
     <i>
       Источник: <a href="https://learn.javascript.ru/websocket">javascript.ru</a>
     </i>
    </p>
  </div>
</details>