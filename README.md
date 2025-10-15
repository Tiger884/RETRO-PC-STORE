# 🎮 RETRO-PC STORE

[![Production Ready](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)](./index.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-3.3.2-blue)](CHANGELOG.md)

> Винтажный магазин ретро-компьютеров эпохи Intel 8086 с современным веб-интерфейсом

## ✨ Возможности

### Функциональность

- 📦 12 демонстрационных товаров Intel 8086/8088/8087
- 🔍 Поиск и фильтрация по категориям
- 🎨 Переключение тем (зеленая/янтарная)
- 🖼️ Smart Image Placeholder система
- 📱 Полностью адаптивный дизайн
- ♿ WCAG 2.1 AA совместимость
- 🚀 Высокая производительность

### Технологии

- 🏗️ Модульная ES6 архитектура
- 🎯 Без внешних зависимостей
- 🔧 DEBUG режим для разработки
- 📝 Семантическая разметка
- 🧹 Оптимизированная структура

## 🚀 Быстрый старт

### Локально

```bash
# Откройте index.html в браузере
```

### GitHub Pages

```bash
# 1. Загрузите на GitHub
# 2. Settings → Pages → Source: main branch
# 3. Сайт: https://username.github.io/repo-name/
```

### С сервером

```bash
# Python
python -m http.server 8080

# Node.js
npx http-server -p 8080

# Vite (dev)
npm install
npm run dev
```

## 📁 Структура

```text
/
├── index.html              # Главная страница
├── placeholder-demo.html   # Демо плейсхолдеров
├── assets/
│   ├── css/main.css       # Единственный CSS
│   ├── js/
│   │   ├── main.js        # Главный скрипт
│   │   └── fallback-data.js
│   └── img/
├── docs/                   # Документация
│   ├── PROJECT_ARCHITECTURE_MAP.md
│   ├── REFACTORING_ROADMAP.md
│   └── IMAGE_PLACEHOLDER_GUIDE.md
└── manifest.json          # PWA манифест
```

## 🎨 Особенности дизайна

### Ретро стиль

- 🖥️ Терминальные цвета (зеленый/янтарный)
- 📟 Моноширинный шрифт Courier New
- ⚡ ASCII-арт декор
- 🔲 Pixel perfect границы

### Современность

- 🔄 Плавные анимации
- 📱 Responsive layout
- 🎯 Touch-friendly интерфейс
- ♿ Полная доступность

## 🛠️ Разработка

### DEBUG режим

В `assets/js/main.js` строка 11:

```javascript
const DEBUG = true;  // Включить логи
const DEBUG = false; // Production режим
```

### Сборка

```bash
npm install
npm run build    # Production build
npm run preview  # Preview build
```

## 📊 Производительность

- ⚡ Lighthouse Score: 95+
- 📦 Размер: ~1.5MB (оптимизировано)
- 🚀 Первая загрузка: <2s
- ♿ Accessibility: 100/100

## 📚 Документация

Полная документация в папке `docs/`:

- **PROJECT_ARCHITECTURE_MAP.md** - Архитектура (3800+ строк)
- **REFACTORING_ROADMAP.md** - План развития (2500+ строк)
- **IMAGE_PLACEHOLDER_GUIDE.md** - Гид по плейсхолдерам
- **DEVELOPMENT.md** - Для разработчиков

## 🔄 Обновления

### v3.3.1 (2025-10-14)

- ✅ Удалены дублирующиеся CSS файлы (↓40% размер)
- ✅ Добавлен DEBUG режим для console.log
- ✅ Очищена структура проекта
- ✅ Оптимизирована производительность

Полная история: [CHANGELOG.md](CHANGELOG.md)

## 🤝 Использование

Проект под лицензией MIT - используйте свободно!

## 🎯 Демо

**Онлайн:** [GitHub Pages](https://tiger884.github.io/RETRO-PC-STORE/)  
**Локально:** Откройте `index.html`  
**Плейсхолдеры:** `placeholder-demo.html`

---

Винтажный стиль × Современные технологии

Создано с ❤️ для демонстрации навыков веб-разработки

[Документация](docs/) • [Changelog](CHANGELOG.md) • [License](LICENSE)
