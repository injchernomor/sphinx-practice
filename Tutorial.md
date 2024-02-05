# Инструкция по работе со Sphinx "step by step"
## Создание виртуального окружения и активация Python
```
python3 -m venv .venv
source .venv/bin/activate
```
## Обновление pip
```
pip install --upgrade pip
```

## Создать папку requirements.txt и внести пакеты, которые нужно установить
Содержимое requirements.txt:
sphinx
myst-parser
sphinx-book-theme
```
pip install -r requirements.txt
```

## Создаем папку docs, где хранятся данные Sphinx
```
sphinx-quickstart docs
```
Нажимаем yes

## В терминале ереходим в папку docs, делаем первый HTML файл:
```
make html
```
Проверяем HTML:
```
firefox ..... /docs/build/html/index.html
```

## Настраиваем конфигурацию
Переходим в ./docs/source/conf.py . Меняем на:
```
extensions = ['myst_parser','sphinx.ext.todo','sphinx.ext.viewcode','sphinx.ext.autodoc', 'sphinx.ext.napoleon']

html_theme = 'sphinx_book_theme'
```
В начало файла вставляем:
```
import os
import sys

sys.path.insert(0, os.path.abspath('../../PROJECT-folder-NAME'))
```
Указывает путь к папке с проектом. 

Переходим в папку docs. Ввести команду: 
В команде указываем путь docs/processed-documentation-files (не меняем)(где будут хранится временные файлы от python доков) и путь к проекту с пайтом файлами (меняем).
```
sphinx-apidoc -f -o source/processed-documentation-files ../PROJECT-folder-NAME
```
В IDE processed-documentation-files отображается не сразу. Зайдите через проводник.
Перейти в processed-documentation-files
Добавить в index.rst к modules


```
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   ./processed-documentation-files/modules
```
**В папке с модулем должен быть файл __init__.py, чтобы он обрабатывался!!!**

## Создаем Markdown файл
В source/ папке сделаем файл с названием mymarkdown.md
Добавляем mymarkdown.md в index.rst
Маркдавн фал должен быть не пустым!
```
===========================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

   mymarkdown
   ./processed-documentation-files/modules

Indices and tables
==================
```

```
## Conventional Commits
+ build Сборка проекта или изменения внешних зависимостей
+ ci Настройка CI и работа со скриптами
+ docs Обновление документации
+ feat Добавление нового функционала
+ fix	Исправление ошибок
+ perf Изменения направленные на улучшение производительности
+ refactor Правки кода без исправления ошибок или добавления новых функций
+ revert Откат на предыдущие коммиты
+ style Правки по кодстайлу (табы, отступы, точки, запятые и т.д.)
+ test Добавление тестов