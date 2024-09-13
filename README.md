# Подключение оплаты 
Приходится писать док-ю в блокноте из-за ограниченности во времени и ресурсах 
## Стек
Бэк: Node.js + Express.js + Mongo.DB
Фронт: Next.js 
## Ключевая структура
### crm-poizzon-api
├── __controllers__ - обработка запросов
  
  ├── __payHandlerOnePay.js__ - сюда приходит подтверждение об оплате. Этот код подтверждает его и меняет статус в заказе. Там же происходит проверка на сплит, на экспресс-доставку. В зависимости от суммы оплаты, пример можно посмотреть в этом файлике
  
  ├── __payOnePay.js__ - создание платежных ссылок, просмотр информации и т.д. Работает как прокси. С клиента прилетает запрос на сервер, сервер обрабатывает данные и просит у платежки создать ссылки


├── __routes__ - пути, на которые должны приходить запрос 


├── __models__ - модели 


### crm-poizon-front
├── __src__
  ├── __components__ - реакт-компоненты
  ├── __store__ - файлы стейт-менеджера MobX
  ├── __types__ - интерфейсы TypeScript
  ├── __utils__ - запросы к API, примеры можно посмотреть в PaySystem.ts 
## Бэк
Настраиваем все на бэке, в структуре описано, где можно найти примеры. Тут проблем возникнуть не должно 
## Фронт
Алгоритм следующий: 
- При создании заказа создавать запросы на создание ссылок. На фронте, __src/components/CreateOrder__ есть метод __handleSubmitCreate()__. Он харкодный, ссылок создается много, очень важно правильно указывать сумму (сплит, полная оплата). Если по нему возникнут вопросы, а они обязательно будут - можно задать их мне 
- Заказ создан, ссылки тоже. Успех! Теперь нужно создавать ссылки во вкладке проверки оплаты (это нужно на тот случай, если ссылки необходимо пересоздать). На фронте, __src/components/AcceptPayment__, метод __handlePayLinkSubmit()__ и т.д (честно, не помню, может быть там есть методы для спплита и экспресс-доставки). Еще на этой странице есть модальные окна подтверждения и аккордеоны. Поэтому придется немного разобраться
- Некст. Нужно вывести кнопочки на странице клиента. На фронте, __src/components/Order__, методы __payLinkRedirect()__, __payLinkSplitRedirect()__, __payLinkSplitSecondRedirect()__, __payLinkExpressRedirect()__ и т.д, они идут подряд. Еще в этих методах проходит проверка на валидность ссылки, стоит обратить на это ванимсние. В разметке тоже необходимо ввести кнопочки оплаты. Кнопочки можно найти по классу __"order__pay-button"__
 
На этом должно быть все
