---
title: "Task Manager - Vue 3 + Python FastAPI"
date: 2026-01-03T17:30:00+03:00
draft: false
type: "reports"
weight: 5
---

## 1. Титульная часть

**Автор:** Арина Самарина  
**Группа:** Р3468  
**Дата:** 03.01.2026  
**Название работы:** Разработка SPA-приложения на Vue 3 с сервером на Python

## 2. Цель работы

Освоить фундаментальные возможности Vue 3 для создания современных одностраничных приложений (SPA), включая работу с реактивными данными, компонентами, маршрутизацией и взаимодействием с сервером. Изучить основы серверной разработки на Python с использованием FastAPI и освоить контейнеризацию приложений с помощью Docker.

**Основные задачи:**
- Изучить синтаксис и структуры Vue 3 (Composition API)
- Освоить работу с реактивностью (ref, reactive, computed, watch)
- Научиться создавать переиспользуемые компоненты с props и событиями
- Изучить систему слотов (обычные, именованные, с ограниченной областью видимости)
- Освоить маршрутизацию с Vue Router
- Научиться работать с формами и валидацией
- Изучить взаимодействие с REST API
- Освоить создание серверной части на Python (FastAPI)
- Изучить контейнеризацию приложений с Docker

## 3. Реализованный функционал

### Клиентская часть (Vue 3)

#### Компоненты:

1. **AppHeader.vue** - Верхнее меню навигации
   - Фиксированное позиционирование при скролле
   - Навигационные ссылки с активным состоянием
   - Адаптивный дизайн

2. **AppFooter.vue** - Нижняя панель
   - Динамический год (вычисляется автоматически)
   - Информация о технологиях проекта

3. **TaskList.vue** - Список задач с фильтрацией и сортировкой
   - Отображение списка задач через v-for
   - Фильтрация по статусу (все/выполненные/невыполненные)
   - Сортировка по дате добавления и алфавиту
   - Условный рендеринг пустого списка (v-if)
   - Передача событий от дочернего компонента к родительскому
   - Интеграция с компонентами загрузки (SkeletonLoader, Spinner)

4. **TaskItem.vue** - Отображение одной задачи
   - Принимает props (task)
   - Отображает заголовок, описание, метаданные
   - Бейджи приоритета, категории и важности
   - Кнопки действий с событиями (@delete, @toggle, @edit)
   - Условное отображение статуса задачи

5. **TaskForm.vue** - Форма создания/редактирования задачи
   - Поля: заголовок (input), описание (textarea), приоритет (select), категория (radio), важность (checkbox)
   - Использование v-model с модификаторами (.trim)
   - Валидация полей через watch
   - Обработка создания и редактирования задачи
   - Отправка данных на сервер

6. **LayoutCard.vue** - Компонент с слотами
   - Обычный слот (default) с ограниченной областью видимости
   - Именованные слоты (header, footer)
   - Передача данных через scoped slot

7. **SkeletonLoader.vue** - Компонент для отображения состояния загрузки
   - Анимированные плейсхолдеры вместо текста "Загрузка..."

8. **Spinner.vue** - Компонент спиннера загрузки
   - CSS-анимация вращения

#### Computed и Watch:

**Computed свойства:**
- `filteredTasks` в TaskList.vue - фильтрация задач по статусу
- `sortedTasks` в TaskList.vue - сортировка отфильтрованных задач
- `currentYear` в AppFooter.vue - динамический год

**Watch:**
- Watch на `statusFilter` и `sortBy` в TaskList.vue для отслеживания изменений фильтров
- Watch на `formData.title` и `formData.description` в TaskForm.vue для валидации при вводе

#### Слоты:

1. **Обычный слот (default)** - в LayoutCard.vue для основного контента
2. **Именованный слот** - `header` и `footer` в LayoutCard.vue
3. **Слот с ограниченной областью видимости** - передача данных `cardData` в default слот LayoutCard.vue

Пример использования:
```vue
<LayoutCard>
  <template #header>
    <h2>Заголовок</h2>
  </template>
  
  <template #default="{ data }">
    <p>{{ data.title }}</p>
  </template>
  
  <template #footer>
    <button>Действие</button>
  </template>
</LayoutCard>
```

#### Маршруты:

- `/` - Главная страница (Dashboard) - компонент Home.vue
- `/tasks` - Список задач - компонент Tasks.vue
- `/tasks/new` - Создание новой задачи - компонент TaskNew.vue
- `/tasks/:id/edit` - Редактирование задачи - компонент TaskEdit.vue (динамический маршрут)
- `/:pathMatch(.*)*` - Страница 404 - компонент NotFound.vue (catch-all маршрут)

**Программная навигация:**
- Использование `router.push()` для перехода между страницами
- Использование `route.params` для получения ID задачи
- Использование именованных маршрутов (`name: 'task-edit'`)

### Серверная часть (Python FastAPI)

#### CRUD методы:

- `GET /api/tasks` - Получить все задачи
- `GET /api/tasks/{id}` - Получить задачу по ID
- `POST /api/tasks` - Создать новую задачу
- `PUT /api/tasks/{id}` - Обновить задачу
- `DELETE /api/tasks/{id}` - Удалить задачу

#### Хранение данных:

- Данные хранятся в файле `tasks.json` в корне backend проекта
- При каждом запросе (POST, PUT, DELETE) данные синхронно записываются в файл
- Файл доступен для ручной проверки содержимого

#### Структура проекта:

- `main.py` - основной файл сервера с API endpoints
- `models.py` - модели данных (Task, TaskUpdate) с использованием Pydantic
- `requirements.txt` - зависимости проекта
- `tasks.json` - файл для хранения данных

## 4. Скриншоты интерфейса

### 4.1. Главная страница
Главная страница содержит:
- Hero-секцию с заголовком "Управляйте задачами с легкостью" и описанием
- Кнопку "Начать работу" с анимацией
- Сетку из 4 карточек с функциями приложения (Управление задачами, Умная фильтрация, Гибкая сортировка, Приоритеты)
- Секцию "Как это работает" с пошаговыми инструкциями
- Призыв к действию "Готовы начать? Создайте первую задачу прямо сейчас!" с кнопкой "Создать задачу"
![Главная 1](../images/main1.jpg)
![Главная 2](../images/main2.jpg)
![Главная 3](../images/main3.jpg)

### 4.2. Список задач
Страница списка задач содержит:
- Заголовок "Список задач"
- Блок фильтрации и сортировки:
  - Фильтр по статусу (Все/Выполненные/Невыполненные)
  - Сортировка (По дате добавления/По алфавиту)
  - Кнопка "Создать задачу"
- Список карточек задач с информацией:
  - Заголовок задачи
  - Описание
  - Бейджи приоритета, категории и важности
  - Дата создания
  - Статус (В работе/Выполнено)
  - Кнопки действий (Выполнить/Отменить, Редактировать, Удалить)
![Список задач](../images/list.jpg)

### 4.3. Фильтрация/сортировка
Демонстрация работы фильтров:
- Выпадающий список фильтра по статусу с опциями
- Выпадающий список сортировки с изменением направления стрелки при открытии
![Фильтрация](../images/filter.jpg)
![Сортировка](../images/sort.jpg)

### 4.4. Форма создания
Форма создания новой задачи содержит:
- Заголовок "Новая задача"
- Поле "Заголовок *" (обязательное, валидация минимум 3 символа)
- Поле "Описание *" (обязательное, валидация минимум 10 символов)
- Поле "Приоритет *" (выпадающий список: Низкий/Средний/Высокий)
- Поле "Категория *" (радио-кнопки: Работа/Личное/Разработка)
- Чекбокс "Важно"
- Кнопки "Создать задачу" и "Отмена"
- Отображение ошибок валидации под полями
![Форма создания](../images/create.jpg)

### 4.5. Форма редактирования
Форма редактирования задачи содержит:
- Заголовок "Редактирование задачи"
- Те же поля, что и форма создания, но предзаполненные данными существующей задачи
- Кнопки "Сохранить изменения" и "Отмена"
- Валидация работает так же, как при создании
![Форма редактирования](../images/fix.jpg)

## 5. Пример кода

### 5.1. Использование компонента TaskItem с событиями

```vue
<TaskItem
  v-for="task in sortedTasks"
  :key="task.id"
  :task="task"
  @delete="handleDelete"
  @toggle="handleToggle"
  @edit="handleEdit"
/>
```

### 5.2. Computed свойство для фильтрации и сортировки

```javascript
// фильтрация задач по статусу
const filteredTasks = computed(() => {
  if (statusFilter.value === 'all') {
    return tasks.value
  } else if (statusFilter.value === 'completed') {
    return tasks.value.filter(task => task.completed)
  } else {
    return tasks.value.filter(task => !task.completed)
  }
})

// сортировка отфильтрованных задач
const sortedTasks = computed(() => {
  const filtered = [...filteredTasks.value]
  if (sortBy.value === 'date') {
    // сортировка по дате создания (новые сначала)
    return filtered.sort((a, b) => {
      const dateA = new Date(a.created_at || 0)
      const dateB = new Date(b.created_at || 0)
      return dateB - dateA
    })
  } else if (sortBy.value === 'alphabet') {
    // сортировка по алфавиту
    return filtered.sort((a, b) => a.title.localeCompare(b.title))
  }
  return filtered
})
```

### 5.3. Watch для валидации формы

```javascript
// валидация заголовка при вводе
watch(() => formData.title, (newVal) => {
  if (newVal.length < 3) {
    errors.title = 'Заголовок должен содержать минимум 3 символа'
  } else {
    errors.title = ''
  }
})

// валидация описания при вводе
watch(() => formData.description, (newVal) => {
  if (newVal.length < 10) {
    errors.description = 'Описание должно содержать минимум 10 символов'
  } else {
    errors.description = ''
  }
})
```

### 5.4. Использование слотов

```vue
<LayoutCard>
  <template #header>
    <h2>Как это работает</h2>
  </template>
  
  <template #default="{ data }">
    <div class="workflow-section">
      <p>{{ data.title }}</p>
    </div>
  </template>
  
  <template #footer>
    <div class="footer-cta">
      <p>Готовы начать? Создайте первую задачу прямо сейчас!</p>
      <router-link to="/tasks/new" class="btn btn-create-task">
        Создать задачу
      </router-link>
    </div>
  </template>
</LayoutCard>
```

### 5.5. Условный рендеринг и обработка событий

```vue
<div v-if="sortedTasks.length === 0" class="empty-state">
  <p>Нет задач для отображения</p>
  <router-link to="/tasks/new" class="btn btn-primary">
    Создать первую задачу
  </router-link>
</div>

<div v-else class="tasks-container">
  <TaskItem
    v-for="task in sortedTasks"
    :key="task.id"
    :task="task"
    @delete="handleDelete"
    @toggle="handleToggle"
    @edit="handleEdit"
  />
</div>
```

### 5.6. Работа с формами и v-model

```vue
<input
  id="title"
  v-model.trim="formData.title"
  type="text"
  required
  placeholder="Введите заголовок задачи"
  class="form-input"
  :class="{ error: errors.title }"
/>

<textarea
  id="description"
  v-model.trim="formData.description"
  required
  placeholder="Введите описание задачи"
  class="form-textarea"
  :class="{ error: errors.description }"
></textarea>

<select
  id="priority"
  v-model="formData.priority"
  required
  class="form-select"
>
  <option value="low">Низкий</option>
  <option value="medium">Средний</option>
  <option value="high">Высокий</option>
</select>
```

## 6. JSON данные

Данные хранятся в файле `backend/tasks.json`:

```json
[
  {
    "id": 2,
    "title": "Настроить маршрутизацию в приложении",
    "description": "Реализовать навигацию между страницами с помощью Vue Router",
    "completed": true,
    "priority": "medium",
    "category": "development",
    "important": false,
    "created_at": "2025-12-20T15:30:00"
  },
  {
    "id": 3,
    "title": "Изучить Docker и контейнеризацию",
    "description": "Познакомиться с технологией Docker и научиться создавать контейнеры",
    "completed": false,
    "priority": "low",
    "category": "personal",
    "important": false,
    "created_at": "2025-12-21T09:15:00"
  },
  {
    "id": 4,
    "title": "выспаться",
    "description": "какой-то кошмар со сном, нужно это исправлять",
    "priority": "high",
    "category": "personal",
    "important": true,
    "completed": false,
    "created_at": "2026-01-07T06:31:54.859677"
  }
]
```

## 7. Инструкция по запуску (Docker)

### Требования:
- Docker Desktop (для Windows/Mac) или Docker Engine (для Linux)
- Docker Compose

### Установка Docker:

**Windows:**
1. Скачайте Docker Desktop с официального сайта: https://www.docker.com/products/docker-desktop
2. Установите Docker Desktop
3. Запустите Docker Desktop и дождитесь полной загрузки
4. Проверьте установку: `docker --version`

**Mac:**
1. Скачайте Docker Desktop для Mac: https://www.docker.com/products/docker-desktop
2. Установите и запустите Docker Desktop

**Linux:**
```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install docker.io docker-compose

# Проверка
docker --version
docker compose version
```

### Запуск проекта:

1. **Клонируйте репозиторий**:
```bash
git clone https://github.com/arrsamarina/vue3-python.git
cd vue3-python
```

2. **Соберите Docker образы**:
```bash
docker compose build
```
*Это может занять несколько минут при первом запуске*

3. **Запустите контейнеры**:
```bash
docker compose up
```
*Или в фоновом режиме:*
```bash
docker compose up -d
```

4. **Откройте браузер**:
- **Frontend**: http://localhost:8080
- **Backend API**: http://localhost:8000
- **API документация (Swagger)**: http://localhost:8000/docs
- **Альтернативная документация**: http://localhost:8000/redoc

### Полезные команды:

**Остановка контейнеров:**
```bash
docker compose down
```

**Просмотр логов:**
```bash
docker compose logs -f
```

**Пересборка после изменений:**
```bash
docker compose build --no-cache
docker compose up
```

**Остановка и удаление контейнеров и образов:**
```bash
docker compose down -v --rmi all
```

### Альтернатива: запуск без Docker

Если Docker не установлен, можно запустить проект локально:

**Backend:**
```bash
cd backend
pip install -r requirements.txt
python main.py
```
Backend будет доступен на http://localhost:8000

**Frontend:**
```bash
cd frontend
npm install
npm run dev
```
Frontend будет доступен на http://localhost:3000

*Примечание: В этом случае нужно настроить CORS на бэкенде или использовать proxy в vite.config.js*

## 8. Выводы

В ходе выполнения задания было изучено:

1. **Vue 3 структуры и синтаксис** - освоены основные директивы (v-if, v-for, v-model, v-bind, v-on), реактивность через Composition API (ref, reactive), computed свойства для вычисляемых значений, watch для отслеживания изменений

2. **Компонентный подход** - создание переиспользуемых компонентов с props для передачи данных от родителя к потомку, использование событий ($emit) для передачи данных от потомка к родителю, организация компонентов в иерархическую структуру

3. **Маршрутизация** - настройка Vue Router с использованием createRouter и createWebHistory, работа с динамическими маршрутами через параметры (:id), программная навигация через router.push(), обработка несуществующих маршрутов через catch-all маршрут

4. **Работа с формами** - использование v-model для двусторонней привязки данных, применение модификаторов (.trim), реализация валидации через watch и условный рендеринг ошибок, обработка различных типов полей (input, textarea, select, radio, checkbox)

5. **API-взаимодействие** - работа с REST API через fetch API, создание сервисного слоя для инкапсуляции API-запросов, обработка асинхронных операций (async/await), обработка ошибок и состояний загрузки

6. **Работа с Docker** - создание Dockerfile для фронтенда (многоэтапная сборка с Node.js и Nginx) и бэкенда (Python с uvicorn), настройка docker-compose.yml для оркестрации контейнеров, использование volumes для сохранения данных, настройка сетевого взаимодействия между контейнерами

7. **Структурирование SPA-проекта** - организация кода по компонентам, views, services, router, разделение ответственности между компонентами, использование композиции компонентов

8. **Слоты** - использование обычных слотов для передачи контента в компоненты, именованных слотов для структурированного контента (header, footer), слотов с ограниченной областью видимости для передачи данных из дочернего компонента в родительский

9. **Серверная разработка на Python** - создание REST API с использованием FastAPI, работа с моделями данных через Pydantic, реализация CRUD-операций, работа с JSON файлами для хранения данных, настройка CORS для взаимодействия с фронтендом

10. **UI/UX дизайн** - создание современного интерфейса с темной темой, реализация адаптивного дизайна для мобильных устройств, использование анимаций и переходов для улучшения пользовательского опыта, типографика и работа с висячими союзами и предлогами

## Ссылка на репозиторий

https://github.com/arrsamarina/vue3-python

## Структура проекта

```
/
├── frontend/              # Vue 3 клиентское приложение
│   ├── src/
│   │   ├── components/    # Vue компоненты
│   │   │   ├── AppHeader.vue
│   │   │   ├── AppFooter.vue
│   │   │   ├── TaskList.vue
│   │   │   ├── TaskItem.vue
│   │   │   ├── TaskForm.vue
│   │   │   ├── LayoutCard.vue (с слотами)
│   │   │   ├── SkeletonLoader.vue
│   │   │   └── Spinner.vue
│   │   ├── views/         # Страницы
│   │   │   ├── Home.vue
│   │   │   ├── Tasks.vue
│   │   │   ├── TaskNew.vue
│   │   │   ├── TaskEdit.vue
│   │   │   └── NotFound.vue
│   │   ├── router/        # Маршрутизация
│   │   │   └── index.js
│   │   ├── services/      # API сервисы
│   │   │   └── api.js
│   │   ├── App.vue
│   │   └── main.js
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   ├── Dockerfile
│   └── nginx.conf
│
├── backend/               # FastAPI сервер
│   ├── main.py           # Основной файл сервера
│   ├── models.py         # Модели данных
│   ├── requirements.txt
│   ├── tasks.json        # Хранилище данных
│   └── Dockerfile
│
├── docker-compose.yml    # Оркестрация контейнеров
└── README.md            # Документация проекта
```

## Технологии

### Frontend:
- Vue 3 (Composition API)
- Vue Router 4
- Vite
- Nginx (для продакшн)

### Backend:
- Python 3.11
- FastAPI
- Uvicorn
- Pydantic

### DevOps:
- Docker
- Docker Compose
