# Tender Hack: Нижний Новгород
## Цель и задачи

Разработка прототипа механизма поиска товаров на портале поставщиков

**В рамках хакатона участникам предстоит реализовать задачи:**
Проанализировать типовой функционал системы поиска товаров (поиск по ходу набора названия – подсказки, контекстные синонимы, транслитерация, опечатки, ранжирование подсказок и выдачи, поиск с учетом свойств, учет перестановки слов, история поиска, аналогичные товары и т.д.);
Изучить исходные данные для понимания возможной глубины поиска, критериев будущей выдачи и прочих взаимосвязей;
Предварительно обработать данные в удобные структуры для работы системы;
Выявить типовые метрики качества и эффективности системы;
Реализовать систему;
Провести тестирование системы, оптимизировать ее работу в рамках улучшения метрик;
Продемонстрировать работоспособность проекта;
Определить возможности по масштабированию решения и следующим его доработкам;
Презентовать проект.

## Решение

![scheme](https://github.com/EugGolovanov/Zakupki/blob/main/images/app-work-2.jpg)

Проект представляет из себя комбинаицю самых свежих практик и технологий,\
благодаря чему способен производить поиск закупок и работ параллельно с сопутсвующими товарами менее чем за пол секундуы!

Проект разработан так, что масштабируемость происходит нативно. При увеличении объема данных, скорость упадет, но совсем незначительно. Мы используем FAISS, разработку которую применяют на детекции лиц и сопоставлении им профилей на более чем 12 миллионов картинок.

Подробнее - [FAISS: Быстрый поиск лиц и клонов на многомиллионных данных](https://habr.com/ru/company/dentsuRU/blog/509204/)

Если в наших руках окажутся данные с парами вместе с A купил B, то мы сможем значительно улучшить качество ранжирования.

Приложение адаптировано как под стационарные компьютеры, ноутбуки,\
так и под мобильные телефоны. Используется фреймворк streamlit.

Мы производим оптимизацию потребления ресурсов диска при работе с эмбеддингами, благодаря использованию бинарного формата feather. 900 мб на диске и около 5 сек на прочтение. Эмбеддинги (350к строк * 768 dim) занимают в памяти, в fp16 порядка 600-700мб.

Если бы хранили эмбеддинги в csv, то время прочтения составило ~30 сек, а объем на диске порядка 3-4 гб.

В качестве моделей используется LABSE.

Таким образом проект портебляет порядка 5-6 гб оперативной памяти, и способен выполняться на одном ядре CPU без использования GPU. Все в купе позволяет экономить на содержании продукта, что немало важно при реальном использовании.


## Полезное:
[Данные](https://github.com/EugGolovanov/Zakupki/tree/main/data)\
[Как запустить локально (on Windows 11)](https://github.com/EugGolovanov/Zakupki/tree/main/streamlit-app)\
[Кодовая база для обучения](https://github.com/EugGolovanov/Zakupki/tree/main/notebooks)
