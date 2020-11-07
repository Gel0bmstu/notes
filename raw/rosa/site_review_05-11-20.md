site_review_05-11-20

## Проблемы интерфейса

1. На главной странице в разделе абитуриенты ссылка "Шаг в будующее" некликабельная. Ссылка должна вести на *http://iu2.bmstu.ru//study/step.html*
![shag_v_buduyshee](https://i.imgur.com/JM7nZUZ.png)

2. На главной странице фотоколлаж "Сотрудники" ведет на главную старницу, должен вести на *http://iu2.bmstu.ru/department/staff.html*
![staff](https://i.imgur.com/jpaLbvs.png)

3. На главной странице фотоколлаж "Разработки" не открывается.
![dev](https://i.imgur.com/mvOwVM7.png)

4. По ссылке *http://iu2.bmstu.ru/department/hystory.html* в блоке "История кафедры" и "Выдающиеся выпускники и деятели кафедры" съехала верстка:
![zavcaf](https://i.imgur.com/owlxG6v.png)

5. В блоке "Учебная деятельность" страницы "Абитуриенту" (*http://iu2.bmstu.ru/study/step.html*) и учебная литература не заполнены.
![abitur](https://i.imgur.com/BswrY5Y.png)
![liter](https://i.imgur.com/sinu5cC.png)

6. Блок "Научная деятельность" (*http://iu2.bmstu.ru/science/foreign.html*) полностью пустой.

7. Блок "Контакты" (*http://iu2.bmstu.ru/contacts/contacts.html*) не открывается.

8. В блоке "Учебная деятельность" в разделе "Дисциплины" *http://iu2.bmstu.ru/study/pract.html* таблица не вмещается в экран:
![pract](https://i.ibb.co/qCWsrRV/screenshoot.png)

## Проблемы с контентом

- Большинство ссылок битые ;
- Много заглушек;
- Нет методичек к лабораторкам;
- Весь контент устарел (старые расписания, список научруков по студентам и тд).

## Проблемы архитектуры

Этот блок необходимо направить разработчикам сайта.

- Сайт не SPA;
- Нет кеширования страниц;
- Сайт не адаптирован под мобильные устройства;
- Запросы на документы должны проксироваться на nginx;
- Сами документы (.doc, .pdf) почему-то лежат в папке /img/.
- Страница "Дисциплина" (*http://iu2.bmstu.ru/study/pract.html*) зачем-то пытается загрузить фото Коновалова:
![konovalov](https://i.ibb.co/cyXHvWm/screenshoot.png)
эта *figure* вообще здесь не нужена:
![figure](https://i.ibb.co/8bFM0zs/screenshoot.png)

