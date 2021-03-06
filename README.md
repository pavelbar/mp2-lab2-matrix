﻿Рабочий процесс

**git status**

**git add :/**

**git commit -m "name"**

**git status**

git push -u myserver master

__________________________________________________________________
удалить файл из индекса

git update-index --assume-unchanged FILENAME
__________________________________________________________________
 обратная команда, для возвращения в индекс:

git update-index --no-assume-unchanged FILENAME
__________________________________________________________________
создать ветку и сразу же перейти на неё

git checkout -b iss53

Это сокращение для:
git branch iss53          -создать
git checkout iss53        -перейти
__________________________________________________________________
инициализтровать хранилище
git init
__________________________________________________________________

 Просмотреть кофиг
 
git config --list
__________________________________________________________________
 Задать имя 
 
git config --global user.name "pavelbar"
__________________________________________________________________
 Задать почту
 
git config --global user.email pavelbaranow@gmail.com
__________________________________________________________________
 Клонируем репозиторий
 
git clone https://github.com/pavelbar/Laboratory-work-1-bit-field-
__________________________________________________________________
 Путь в настоящее время
 
pwd
__________________________________________________________________
 Перейти в каталог C: /project
 
cd /c/1_lab_work/Laboratory-work-1-bit-field-/
__________________________________________________________________
 Что изменили и не проиндексировали
 
git diff
__________________________________________________________________
 что вы проиндексировали и что войдёт в следующий коммит
 
git diff --staged

git diff --cached
__________________________________________________________________
 Создать коммит
 
git commit -m "comment"
__________________________________________________________________
 Просмотреть, какие удалённые серверы у вас уже настроены (-v с адресами)
 
git remote -v
__________________________________________________________________
 Добавить репозиторий
 
git remote add [сокращение] [url]

git remote myserver https://github.com/pavelbar/Laboratory-work-1-bit-field- 
__________________________________________________________________
 Fetch - (нет)  извлекает и не сливает данные из удалённой ветки в текущую ветку
 
git fetch [имя удал. сервера]
__________________________________________________________________
 Pull - (да) извлекает и сливает данные из удалённой ветки в вашу текущую ветку. 
 
git pull [имя удал. сервера]
__________________________________________________________________
 Push -  отправить изменения в главный репозиторий
 
git push [удал. сервер] [ветка]
__________________________________________________________________
 Удалить ссылку 
 
git remote rm [origin]
__________________________________________________________________
# Методы программирования 2: Верхнетреугольные матрицы на шаблонах

[![Build Status](https://travis-ci.org/UNN-VMK-Software/mp2-lab1-set.svg)][travis]

<!-- TODO
  -
-->

## Цели и задачи

В рамках лабораторной работы ставится задача создания программных средств, поддерживающих эффективное хранение матриц специального вида (верхнетреугольных) и выполнение основных операций над ними:

- сложение/вычитание;
- копирование;
- сравнение.

В процессе выполнения лабораторной работы требуется использовать систему контроля версий [Git][git] и фрэймворк для разработки автоматических тестов [Google Test][gtest].

Перед выполнением работы студенты получают данный проект-шаблон, содержащий следующее:

 - Интерфейсы классов Вектор и Матрица (h-файл)
 - Начальный набор готовых тестов для каждого из указанных классов.
 - Набор заготовок тестов для каждого из указанных классов. 
 - Тестовый пример использования класса Матрица

Выполнение работы предполагает решение следующих задач:

  1. Реализация методов шаблонного класса `TVector` согласно заданному интерфейсу.
  1. Реализация методов шаблонного класса `TMatrix` согласно заданному интерфейсу.
  1. Обеспечение работоспособности тестов и примера использования.
  1. Реализация заготовок тестов, покрывающих все методы классов `TVector` и `TMatrix`.
  1. Модификация примера использования в тестовое приложение, позволяющее задавать матрицы и осуществлять основные операции над ними.

## Используемые инструменты

  - Система контроля версий [Git][git]. Рекомендуется использовать один из
    следующих клиентов на выбор студента:
    - [Git](https://git-scm.com/downloads)
    - [GitHub Desktop](https://desktop.github.com)
  - Фреймворк для написания автоматических тестов [Google Test][gtest]. Не
    требует установки, идет вместе с проектом-шаблоном.
  - Среда разработки Microsoft Visual Studio (2008 или старше).
  - Опционально. Утилита [CMake](http://www.cmake.org) для генерации проектов по
    сборке исходных кодов. Может быть использована для генерации решения для
    среды разработки, отличной от Microsoft Visual Studio 2008 или 2010, предоставленных в данном проекте-шаблоне.

## Общая структура проекта

Структура проекта:

  - `docs` — инструкции по выполнению лабораторной работы, полезные документы.
  - `gtest` — библиотека Google Test.
  - `include` — директория для размещения заголовочных файлов.
  - `samples` — директория для размещения тестового приложения.
  - `sln` — директория с файлами решений и проектов для VS 2008 и VS 2010,
    вложенные директории `vc9` и `vc10` соответственно.
  - `src` — директория для размещения исходных кодов (cpp-файлы).
  - `test` — директория с модульными тестами и основным приложением,
    инициализирующим запуск тестов.
  - `README.md` — информация о проекте, которую вы сейчас читаете.
  - Служебные файлы
    - `.gitignore` — перечень расширений файлов, игнорируемых Git при добавлении
      файлов в репозиторий.
    - `CMakeLists.txt` — корневой файл для сборки проекта с помощью CMake. Может
      быть использован для генерации проекта в среде разработки, отличной от
      Microsoft Visual Studio.
    - `.travis.yml` — конфигурационный файл для системы автоматического
      тестирования Travis-CI. Тесты, входящие в состав шаблонного проекта,
      регулярно запускаются на удаленной [инфраструктуре][travis].

В решении содержатся следующие модули:

  - Модуль `utmatirx`, содержащий реализацию классов Вектор и Матрица (файл
    `./include/utmatrix.h`). Поскольку оба класса шаблонные, реализацию методов необходимо выполнять непосредственно в заголовочном файле. При этом интерфейсы классов должны
    оставаться неизменными.
  - Тесты для классов Вектор и Матрица (файлы `./test/test_tvector.cpp`, `./test/test_tmatrix.cpp`).
  - Пример использования класса Матрица (файл `./samples/sample_matrix.cpp`).

<!-- LINKS -->

[git]:         https://git-scm.com/book/ru/v2
[gtest]:       https://github.com/google/googletest
[travis]:      https://travis-ci.org/UNN-VMK-Software/mp2-lab1-set

