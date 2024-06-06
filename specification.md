# Техническое задание

## 1. Описание функциональности

### 1.1. Задачи

После загрузки приложения в списке задач отображается не более 8 карточек задач.

Показ оставшихся карточек задач осуществляется с помощью кнопки «Load more». При нажатии в список добавляются очередные 8 задач. Либо оставшиеся задачи, если их количество меньше 8.

Любое изменение фильтра или сортировки сбрасывает счётчик показанных задач и отсчёт начинается заново.

Если все задачи показаны, кнопка «Load more» скрывается.

Если задачи отсутствуют или все задачи выполнены, то вместо списка задач отображается текст: Click «ADD NEW TASK» in menu to create your first task.

Задачи в списке доступны только для просмотра. Для редактирования задачи пользователь нажимает на кнопку «Edit».

В карточке задачи пользователю доступна кнопка «Favorites». При нажатии на кнопку, задача добавляется в избранное. Повторное нажатие приводит к удалению из избранного. При этом сразу же происходит пересчёт количества задач в избранном (см. «Фильтры»).

В карточке пользователю доступна кнопка «Archive». При нажатии на кнопку, задача помечается выполненной. При этом к ней сразу же применяется действие фильтров и сразу же происходит пересчёт количества задач в избранном (см. «Фильтры»).

Повторное нажатие на кнопку «Archive» помечает задачу, как невыполненную. Это действие возможно только при активации фильтра «Archive» (см. «Фильтры»).

Кнопки «Favorites» и «Archive» отражают состояние задачи с помощью установки/удаления css-класса card__btn--disabled.

Просроченным задачам добавляется класс card--deadline. Под просроченной задачей подразумевается задача с установленной датой исполнения меньше текущей даты.

### 1.2. Создание задачи

Новая задача создаётся нажатием на кнопку «Add new task». После нажатия пользователь видит форму создания новой задачи, которую ему необходимо заполнить.

Форма создания новой задачи всегда появляется первой в списке задач. Форма создания «сдвигает» остальные задачи, а не занимает место одной из них. То есть в списке может быть 8 карточек задач плюс форма создания и так далее.

Если в момент нажатия на кнопку «Add new task» был выбран фильтр или применена сортировка, то они сбрасываются на состояния «All» и «SORT BY DEFAULT» соответственно.

Нажатие на клавишу Esc или клик по кнопке «Cancel» приводит к закрытию формы создания задачи без сохранения изменений.

Закрытие формы происходит всегда, кроме случая, когда в момент нажатия Esc фокус стоит в любом поле ввода формы (описание задачи, дата исполнения и т. д.).

Менеджер задач позволяет создавать задачи двух видов:

* задачи без повторения;

* регулярные задачи — повторяемые по определённым дням недели.

Для регулярных задач обязательно должен быть выбран день (дни) недели для повторения и скрыто поле «Дата исполнения». В случае несоблюдения условий задача не может быть сохранена — кнопка «Save» заблокирована;

В форме создания пользователь заполняет поля:

* Описание задачи:
  * минимальная длина 1 символ;
  * максимальная длина 140 символов;
* Дата исполнения:
  * поле может быть не заполнено;
  * дата: число и месяц полностью;
  * скрыто при активированном флаге повторения;
  * выбор даты осуществляется с помощью библиотеки flatpickr.js;
* Флаг повторения:
  * определяет, является ли задача регулярной;
  * значение по умолчанию NO;
  * изменение флага повторения сразу отображается в шапке карточки задачи (до сохранения) — цветная полоска становится волнистой, а не прямой;
  * Дни недели повтора задачи:
    по умолчанию ни один день не выбран;
    отображено, если установлен флаг повторения. В противном случае скрыто;
* Цветовая категория:
  * выбор цветовой категории меняет цвет в шапке задачи путём добавления одного из css-классов: card--black, card--green, card--yellow, card--pink, card--blue;
  * обновление цветовой категории в шапке происходит после сохранения изменений;
  * для задачи может быть установлена только одна цветовая категория;
  * значение по умолчанию: card--black;

Скрытые поля интерпретируются как пустые при сохранении задачи.

Введённые пользователем данные экранируются.

### 1.3. Редактирование задачи

Для редактирования задачи пользователь нажимает кнопку «Edit». В этот момент карточка задачи заменяется на форму редактирования задачи.

В форме редактирования представлены все поля, которые пользователь заполняет при создании новой задачи (см. раздел «Создание задачи»). Правила их поведения сохраняются.

В качестве значений по умолчанию используются фактические данные редактируемой задачи.

Если пользователь не сохранил изменения, то все изменения, включая цветовую категорию, флаг избранного, флаг выполнения сбрасываются после закрытия формы редактирования.

Одновременно в режиме редактирования или создания может находиться только одна задача.

Если у пользователя открыта задача для редактирования/создания и пользователь открывает другую задачу для редактирования/создания, то первая задача переходит в режим просмотра (пропадает в случае создания). Несохраненные данные при этом теряются.

Для сохранения внесённых изменений во время редактирования пользователь нажимает кнопку «Save». Форма редактирования закрывается, пользователь видит задачу в режиме просмотра.

Нажатие на кнопку Esc приводит к закрытию формы редактирования без сохранения изменений. Пользователь видит задачу в режиме просмотра.

Закрытие формы происходит всегда, кроме случая, когда в момент нажатия Esc фокус стоит в любом поле ввода формы (описание задачи, дата исполнения и т. д.).

### 1.4. Фильтры

Для быстрого поиска задач в приложении предусмотрено несколько фильтров:

* All — все невыполненные задачи.
* Overdue — просроченные задачи.
* Today — задачи на сегодня.
* Favorites — избранные задачи.
* Repeating — повторяющиеся задачи.
* Archive — выполненные задачи.

При активации фильтра отображаются только те задачи, которые ему удовлетворяют.

Рядом с названием фильтра отображается число — количество удовлетворяющих этому фильтру задач. Оно обновляется при создании, редактировании, удалении, архивации или добавлении задачи в избранное.

Если задачи удовлетворяющие фильтру отсутствуют, то кнопке установки этого фильтра добавляется атрибут disabled.

Если в момент, когда фильтр был активирован, не осталось ни одной задачи, удовлетворяющей этому фильтру, вместо списка отображается соответствующий текст. Например, если были выбраны задачи на сегодня, но пользователь перенёс все задачи на другой день, в отфильтрованном списке должна появится заглушка «There are no tasks today». Все фразы приведены в файле в директории с разметкой.

Одновременно может быть активирован только один фильтр.

Выполненные задачи отображаются только при активации фильтра «Archive».

### 1.5 Сортировка

Пользователю доступна возможность сортировки задач по дате исполнения в обоих направлениях: от меньшей к большей и наоборот. Для этого пользователю нужно кликнуть по ссылкам «SORT BY DATE up» или «SORT BY DATE down» соответственно.

Для отмены сортировки и возвращению к исходному порядку нужно кликнуть по ссылке «SORT BY DEFAULT».

При смене фильтра сортировка сбрасывается на состояние «SORT BY DEFAULT».

### 1.6 Взаимодействие с сервером

Сервер расположен по адресу https://22.objects.htmlacademy.pro/task-manager.

Спецификация по взаимодействию с сервером в формате OpenAPI — https://22.objects.htmlacademy.pro/spec/task-manager.

Каждый запрос к серверу должен содержать заголовок Authorization со значением Basic ${случайная строка}. Например, Basic er883jdzbdw. Случайная строка формируется однократно при старте приложения.

### 1.7 Обратная связь в интерфейсе

На время загрузки данных вместо списка задач нужно вывести информационное сообщение.

В момент отправки запроса на создание/удаление/изменение задачи форма блокируется от внесения изменений. Разблокировка формы происходит после завершения выполнения запроса (неважно, успешно выполнен запрос или нет).

При создании или редактировании задачи нажатие на кнопку «Save» (а при редактировании ещё и на «Delete») формирует запрос к серверу на сохранение или изменение (а при редактировании ещё и на удаление данных). На время выполнения запроса поля формы и кнопки блокируются, текст заголовка кнопки изменяется:

* Save -> Saving...
* Delete -> Deleting...

В режиме просмотра задачи нажатие на кнопки «Favorites», «Archive» формирует запрос к серверу на изменение данных. На время выполнения запроса кнопки блокируются, текст заголовка кнопки изменяется:

* Favorites -> Favoriting...
* Archive -> Archiving...

Заголовки кнопок возвращаются в исходный вид после выполнения запроса (неважно, успешно выполнен запрос или нет).

Обновление элементов в DOM (удаление задачи, обновление задачи и так далее) происходит только после успешного выполнения запроса к серверу.

Если запрос не удалось выполнить (сервер недоступен, произошла ошибка), форма редактирования/создания остаётся открытой, к ней применяется эффект «покачивание головой».

## 2. Разное

В зависимости от состояния, некоторым элементам управления применяются соответствующие классы оформления. Например, активный фильтр, активный экран, кнопки «Favorites», «Archive» и так далее. Примеры доступны в директории с вёрсткой (markup).