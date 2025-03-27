# Документація Todo List Додатку

## Загальний опис
Todo List - це веб-додаток для управління завданнями, розроблений на React з використанням TypeScript. Додаток дозволяє переглядати список завдань, фільтрувати їх за статусом та шукати за назвою.

## Основні функції
- Перегляд списку завдань
- Фільтрація завдань за статусом (всі/активні/завершені)
- Пошук завдань за назвою
- Перегляд деталей завдання в модальному вікні
- Відображення інформації про користувача для кожного завдання

## Структура проекту
```
src/
├── api/
│   └── index.ts         # API сервіси для роботи з даними
├── components/
│   ├── Loader/          # Компонент завантаження
│   ├── TodoFilter/      # Компонент фільтрації
│   ├── TodoList/        # Компонент списку завдань
│   └── TodoModal/       # Компонент модального вікна
├── types/
│   ├── Todo.ts          # Типи для завдань
│   └── User.ts          # Типи для користувачів
├── App.tsx              # Головний компонент
└── index.tsx            # Точка входу
```

## Компоненти

### App.tsx
Головний компонент додатку, який керує станом та логікою.

**Стан:**
- `todos`: масив завдань [рядки 14-15](src/App.tsx#L14-L15)
- `loading`: стан завантаження [рядки 16-17](src/App.tsx#L16-L17)
- `selectedTodo`: вибране завдання [рядки 18-19](src/App.tsx#L18-L19)
- `selectedUser`: користувач вибраного завдання [рядки 20-21](src/App.tsx#L20-L21)
- `filter`: поточний фільтр [рядки 22-23](src/App.tsx#L22-L23)
- `searchQuery`: пошуковий запит [рядки 24-25](src/App.tsx#L24-L25)
- `modalLoading`: стан завантаження модального вікна [рядки 26-27](src/App.tsx#L26-L27)

**Основні функції:**
- `handleCloseModal`: закриття модального вікна [рядки 29-32](src/App.tsx#L29-L32)
- `handleShowTodo`: відкриття модального вікна з деталями завдання [рядки 34-42](src/App.tsx#L34-L42)
- `filteredTodos`: фільтрація завдань за статусом та пошуковим запитом [рядки 44-52](src/App.tsx#L44-L52)

### TodoList
Компонент для відображення списку завдань.

**Підкомпоненти:**
- `TodoItem`: окремий рядок з завданням [рядки 15-35](src/components/TodoList/TodoList.tsx#L15-L35)

**Функціональність:**
- Відображення ID завдання [рядки 19-20](src/components/TodoList/TodoList.tsx#L19-L20)
- Індикатор завершення [рядки 21-23](src/components/TodoList/TodoList.tsx#L21-L23)
- Назва завдання з кольоровим маркуванням [рядки 24-26](src/components/TodoList/TodoList.tsx#L24-L26)
- Кнопка перегляду деталей [рядки 27-29](src/components/TodoList/TodoList.tsx#L27-L29)

### TodoModal
Модальне вікно для відображення деталей завдання.

**Підкомпоненти:**
- `ModalHeader`: заголовок модального вікна [рядки 15-25](src/components/TodoModal/TodoModal.tsx#L15-L25)
- `ModalContent`: вміст модального вікна [рядки 27-45](src/components/TodoModal/TodoModal.tsx#L27-L45)

**Функціональність:**
- Відображення ID завдання [рядки 30-31](src/components/TodoModal/TodoModal.tsx#L30-L31)
- Назва завдання [рядки 32-33](src/components/TodoModal/TodoModal.tsx#L32-L33)
- Статус завдання (Done/Planned) [рядки 34-35](src/components/TodoModal/TodoModal.tsx#L34-L35)
- Інформація про користувача [рядки 36-40](src/components/TodoModal/TodoModal.tsx#L36-L40)
- Кнопка закриття [рядки 41-43](src/components/TodoModal/TodoModal.tsx#L41-L43)

### TodoFilter
Компонент для фільтрації та пошуку завдань.

**Функціональність:**
- Вибір статусу (all/active/completed) [рядки 15-25](src/components/TodoFilter/TodoFilter.tsx#L15-L25)
- Пошук за назвою [рядки 27-35](src/components/TodoFilter/TodoFilter.tsx#L27-L35)
- Кнопка очищення пошуку [рядки 37-39](src/components/TodoFilter/TodoFilter.tsx#L37-L39)

## API Endpoints

### getTodos
```typescript
const getTodos = async (): Promise<Todo[]> => {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos');
  return response.json();
};
```
[Джерело](src/api/index.ts#L1-L5)

### getUser
```typescript
const getUser = async (userId: number): Promise<User> => {
  const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
  return response.json();
};
```
[Джерело](src/api/index.ts#L7-L11)

## Оптимізації

### Мемоізація
- Використання `useCallback` для функцій [рядки 29-32](src/App.tsx#L29-L32)
- Мемоізація компонентів через `React.memo` [рядки 37-39](src/App.tsx#L37-L39)
- Оптимізована фільтрація даних [рядки 44-52](src/App.tsx#L44-L52)

### Рендеринг
- Умовний рендеринг компонентів [рядки 54-56](src/App.tsx#L54-L56)
- Оптимізоване відображення списку [рядки 58-62](src/App.tsx#L58-L62)
- Ефективна робота з модальним вікном [рядки 64-70](src/App.tsx#L64-L70)

### Стилізація
- Використання Bulma CSS фреймворку [рядки 3-4](src/App.tsx#L3-L4)
- Іконки Font Awesome [рядки 3-4](src/App.tsx#L3-L4)
- Адаптивний дизайн

## Тестування
- Unit тести для компонентів [рядки 1-10](src/App.test.tsx#L1-L10)
- Інтеграційні тести [рядки 12-20](src/App.test.tsx#L12-L20)
- Тестування API взаємодії [рядки 22-30](src/App.test.tsx#L22-L30)

## Стилізація
- Використання Bulma CSS фреймворку [рядки 3-4](src/App.tsx#L3-L4)
- Іконки Font Awesome [рядки 3-4](src/App.tsx#L3-L4)
- Адаптивний дизайн
- Анімації для модального вікна [рядки 1-15](src/components/TodoModal/TodoModal.scss#L1-L15)

## Вимоги до середовища
- Node.js 14+
- npm або yarn
- Современний веб-браузер

## Встановлення та запуск
1. Клонуйте репозиторій
2. Встановіть залежності: `npm install`
3. Запустіть проект: `npm start`
4. Відкрийте http://localhost:3000

## Технічні деталі
- React 18
- TypeScript
- Bulma CSS
- Font Awesome
- Jest для тестування
- ESLint для лінтування
- Prettier для форматування
