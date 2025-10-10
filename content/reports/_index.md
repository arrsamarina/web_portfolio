+++
draft = false
title = 'report #1'
+++
# Лабораторная работа: Работа с Git  
**Студент:** Арина  
**Группа:** PЗ468  

---

## Цель работы
Освоить базовые команды **Git** для работы с локальными и удалёнными репозиториями.  
Научиться выполнять основные операции — инициализацию, добавление файлов, создание коммитов, ветвление и слияние — как в терминале, так и через графический клиент **GitHub Desktop**.

---

## Подготовка окружения
1. Установлен Git и **GitHub Desktop**.  
2. Создана папка `test_repo_for_web` — локальный репозиторий для экспериментов.  
3. Настроено подключение к удалённому репозиторию GitHub.

---

## Ход выполнения

### 1. Создание репозитория
Создана новая папка:
```bash
test_repo_for_web
```
В ней будет находиться локальный репозиторий Git.  
Команда:
```bash
git status
```
показала, что репозиторий пуст, коммитов нет, ветка `master`.

![Шаг 1](images/image22.png)


---

### 2. Создание файла и первый коммит
Создан новый пустой файл:
```powershell
New-Item README.txt -ItemType File
Add-Content README.txt "привет!"
```
![Шаг 2](images/image42.png)
![Шаг 3](images/image7.png)
Файл появился как *untracked*.  
Добавление и фиксация изменений:
```bash
git add README.txt
git commit -m "first file"
```
![Шаг 4](images/image41.png)
![Шаг 5](images/image39.png)


---

### 3. Изменение и добавление нескольких файлов
Добавлен текст в файл:
```powershell
Add-Content README.txt "привет, мир!"
```
Git отмечает `README.txt` как *modified*.  
Добавлены все `.txt` файлы:
```bash
git add '*.txt'
```
![Шаг 6](images/image35.png)
Создан новый файл `README-ENG.txt`, затем:
```bash
git commit -m "all files with .txt extension were added"
```
Изменены 2 файла: добавлен `README-ENG.txt`, обновлён `README.txt`.
![Шаг 7](images/image38.png)
![Шаг 8](images/image40.png)
![Шаг 9](images/image21.png)
---

### 4. Просмотр истории
```bash
git log
git log --summary
```
Отображена история коммитов и подробности изменений.
![Шаг 10](images/image28.png)
![Шаг 11](images/image23.png)
---

### 5. Добавление удалённого репозитория и push
```bash
git remote add origin <URL_репозитория>
git push -u origin master
```
После добавления строк:
```powershell
Add-Content README.txt "hello!"
Add-Content README-ENG.txt "world!"
```
![Шаг 12](images/image32.png)
и выполнения:
```bash
git add '*.txt'
git commit -m "all files with .txt extension were changed"
git push -u origin master
```
локальная ветка `master` синхронизирована с `origin/master`.
![Шаг 13](images/image25.png)
---

### 6. Получение изменений и сравнение версий
```bash
git pull origin master
git diff HEAD
```
После добавления строки `"hello!"` в `README.txt` Git показал зелёную строку `+hello!`, означающую новое добавление.
![Шаг 14](images/image33.png)
![Шаг 15](images/image2.png)
---

### 7. Работа с папками и файлами
Создана структура:
```bash
mkdir folder
New-Item folder/file.txt -ItemType File
```
![Шаг 16](images/image16.png)
Git сообщает:
- `README.txt` — изменён (modified),
- `folder/` — неотслеживается (untracked).

Добавление в индекс:
```bash
git add README.txt folder/.
```

---

### 8. Проверка staged-изменений и отмена
```bash
git diff --staged
git reset folder/file.txt
git diff
git checkout -- README.txt
```
Файл `README.txt` возвращён к последнему зафиксированному состоянию.  
В репозитории осталась только неотслеживаемая папка `folder/`.
![Шаг 17](images/image43.png)
![Шаг 18](images/image34.png)
---

### 9. Работа с ветками
Создание и переход:
```bash
git branch clean_up
git branch
git checkout clean_up
```
![Шаг 19](images/image6.png)
![Шаг 20](images/image14.png)
Удаление и фиксация:
```bash
rm -r folder
git rm README-ENG.txt
git commit -m "deleted folder and files"
```
![Шаг 21](images/image37.png)
![Шаг 22](images/image11.png)
![Шаг 23](images/image10.png)
Возврат и слияние:
```bash
git checkout master
git merge clean_up
git push
```
Изменения из `clean_up` успешно объединены с `master`.

---

## Работа через GitHub Desktop

### 1. Создание нового репозитория  
Создан новый репозиторий прямо из GitHub Desktop.  
![Шаг 24](images/image31.png)
![Шаг 25](images/image9.png)
---

### 2. Добавление файлов  
В проводнике добавлен файл `README.txt`.  
Сделан первый коммит — изменения отображаются во вкладке **Changes** и **History**.  
![Шаг 26](images/image5.png)

---

### 3. Изменение и коммит  
Добавлен новый файл `README-ENG.txt`, изменён `README.txt`.  
Закоммичено и опубликовано на GitHub.  
![Шаг 27](images/image1.png)
![Шаг 28](images/image19.png)

---

### 4. Работа с ветками  
- Создана ветка `clean_up`  
- Удалён файл `README-ENG.txt`  
- Переключение обратно на `main`  
- Выполнен merge ветки `clean_up` в `main`  
- Изменения запушены  
![Шаг 29](images/image17.png)

---

### 5. Итоговый вид репозитория  
На GitHub отображаются все изменения: история коммитов, удаление файлов и актуальное состояние ветки `main`.  
![Шаг 30](images/image15.png)

---

## Результаты
- Изучены и применены команды:  
  `git init`, `git add`, `git commit`, `git log`, `git diff`, `git branch`, `git merge`, `git push`, `git pull`, `git rm`.  
- Получены навыки работы с ветками и индексом.  
- Освоен интерфейс **GitHub Desktop** и работа с удалённым репозиторием.

---

## Вывод
В ходе лабораторной работы были освоены базовые принципы работы с системой контроля версий Git.  
Закреплены практические навыки работы в терминале и графическом клиенте.  
Процесс синхронизации с GitHub отработан полностью — от создания репозитория до push-коммитов и работы с ветками.

---

## Приложение
Для оформления отчёта использован формат **Markdown (.md)**.  



