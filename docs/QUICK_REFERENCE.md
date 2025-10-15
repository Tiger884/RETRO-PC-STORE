# 📚 СПРАВОЧНИК ПРОЕКТА - БЫСТРЫЙ ДОСТУП

> **Создано:** 14 октября 2025  
> **Назначение:** Быстрая навигация по документации проекта

---

## 📖 ДОКУМЕНТАЦИЯ

### 🗺️ **Архитектурная карта** → `docs/PROJECT_ARCHITECTURE_MAP.md`
**Что внутри:**
- Полная структура проекта с графами
- Блочная архитектура (8 основных блоков)
- Зависимости и потоки данных
- Критические точки для рефакторинга

**Когда использовать:**
- Нужно понять как работает проект
- Перед началом любых изменений
- Для onboarding новых разработчиков

---

### 🚀 **Дорожная карта рефакторинга** → `docs/REFACTORING_ROADMAP.md`
**Что внутри:**
- 8 фаз модернизации с детальными инструкциями
- Примеры кода для каждой фазы
- Оценка рисков и способы отката
- Метрики успеха

**Когда использовать:**
- Готовы начать рефакторинг
- Нужна пошаговая инструкция
- Планирование спринтов

---

### 📋 **README** → `README.md`
**Что внутри:**
- Демонстрационные товары
- Инструкции по запуску
- Технические характеристики
- Готовность к демонстрации

**Когда использовать:**
- Первое знакомство с проектом
- Проверка финального состояния

---

### 🛠️ **Руководство разработчика** → `docs/DEVELOPMENT.md`
**Что внутри:**
- Fluid Design System
- Адаптивные брейкпоинты
- Система тем
- Оптимизация и безопасность v3.1

**Когда использовать:**
- Работа с CSS/стилями
- Настройка адаптивности
- Оптимизация производительности

---

### 📝 **План модернизации** → `ПЛАН_МОДЕРНИЗАЦИИ.md`
**Что внутри:**
- Недельный план работ
- Критерии успеха
- Зависимости и ресурсы

**Когда использовать:**
- Планирование времени
- Оценка трудозатрат

---

## 🎯 БЫСТРЫЙ СТАРТ

### 1️⃣ Изучить проект (1-2 часа)
```bash
# Прочитать в порядке:
1. README.md                               # Что это и как работает
2. docs/PROJECT_ARCHITECTURE_MAP.md        # Как устроено внутри
3. docs/REFACTORING_ROADMAP.md             # Как будем улучшать
```

### 2️⃣ Запустить проект (5 минут)
```bash
# Вариант 1: Простое открытие
Двойной клик на index.html

# Вариант 2: Dev server
npm run dev           # http://localhost:3000

# Вариант 3: Production preview
npm run build
npm run preview
```

### 3️⃣ Начать рефакторинг
```bash
# Создать ветку
git checkout -b refactor/phase-1-infrastructure

# Следовать инструкциям
Открыть docs/REFACTORING_ROADMAP.md → Фаза 1
```

---

## 🔍 НАВИГАЦИЯ ПО КОДУ

### HTML
```
index.html
├── Шапка (<header>)
├── Основной контент (<main>)
│   └── Каталог товаров (#products-container)
├── Футер (<footer>)
└── Модалка Wiki (#wiki-modal)
```

### CSS
```
assets/css/main.css
├── CSS переменные (темы)
├── Базовые стили
├── Компоненты (карточки, модалки)
├── Адаптивность
└── Accessibility
```

### JavaScript
```
assets/js/
├── main.js                    # Главное приложение
│   ├── window.retroApp
│   ├── Инициализация
│   ├── Рендеринг товаров
│   ├── Управление темами
│   └── Модальные окна
│
└── fallback-data.js          # Демо данные
    ├── window.fallbackProducts (12 товаров)
    ├── window.imageFormatDetector
    ├── window.productUtils
    └── window.imageUtils
```

---

## ⚡ ЧАСТЫЕ ЗАДАЧИ

### Изменить тему по умолчанию
```javascript
// assets/js/main.js → setupThemeToggle()
const savedTheme = localStorage.getItem('retro-theme') || 'amber'; // Было 'green'
```

### Добавить товар
```javascript
// assets/js/fallback-data.js
window.fallbackProducts.push({
    id: 'new-product',
    title: "Новый товар",
    currentPrice: "$99.99",
    // ... остальные поля
});
```

### Изменить цвета темы
```css
/* assets/css/main.css */
:root[data-theme="green"] {
    --terminal-primary: #33FF33; /* Изменить здесь */
}
```

### Отключить Service Worker
```html
<!-- index.html, строка ~160 -->
<!--
if ('serviceWorker' in navigator) { ... }
-->
```

---

## 🐛 ОТЛАДКА

### Проблема: Товары не отображаются
```javascript
// Проверить в консоли:
console.log(window.fallbackProducts);      // Должен быть массив из 12 элементов
console.log(window.retroApp.products);     // Должен быть такой же массив
console.log(window.retroApp.initialized);  // Должно быть true
```

### Проблема: Тема не переключается
```javascript
// Проверить в консоли:
localStorage.getItem('retro-theme');       // 'green' или 'amber'
document.documentElement.getAttribute('data-theme'); // Должно совпадать

// Очистить кеш:
localStorage.removeItem('retro-theme');
location.reload();
```

### Проблема: Стили не применяются
```html
<!-- Проверить Network tab в DevTools -->
<!-- Должен загружаться: assets/css/main.css -->
<!-- Status: 200 OK -->
```

---

## 📊 СТРУКТУРА ДАННЫХ

### Товар (Product)
```javascript
{
    id: "intel-8086-vintage",              // Уникальный ID
    title: "Intel 8086 CPU...",            // Название
    currentPrice: "$89.99",                // Цена
    condition: "Used - Excellent",         // Состояние
    location: "Silicon Valley, CA",        // Место
    brand: "Intel",                        // Производитель
    yearManufactured: "1978",              // Год выпуска
    
    images: {
        avif: "path/to/image.avif",        // AVIF формат
        webp: "path/to/image.webp",        // WebP формат
        jpg: "path/to/image.jpg",          // JPG формат (fallback)
        alt: "Описание изображения"        // Alt текст
    },
    
    seoMetadata: {
        description: "...",                // SEO описание
        keywords: [...],                   // Ключевые слова
        category: "Vintage Processors"     // Категория
    },
    
    specifications: {
        architecture: "x86 16-bit",        // Характеристики
        frequency: "5-10 MHz",
        // ...
    }
}
```

---

## 🎨 ДИЗАЙН-СИСТЕМА

### Цвета
```css
/* Зеленая тема */
--terminal-bg: #0D0D0D          /* Фон */
--terminal-primary: #33FF33      /* Основной цвет */
--terminal-secondary: #00FF00    /* Вторичный цвет */
--terminal-dim: #00AA00          /* Приглушенный */

/* Янтарная тема */
--terminal-primary: #FFB000      /* Основной цвет */
--terminal-secondary: #FFA500    /* Вторичный цвет */
```

### Отступы
```css
--spacing-xs: clamp(0.25rem, 1vw, 0.5rem)   /* 4-8px */
--spacing-sm: clamp(0.5rem, 2vw, 1rem)       /* 8-16px */
--spacing-md: clamp(1rem, 3vw, 1.5rem)       /* 16-24px */
--spacing-lg: clamp(1.5rem, 4vw, 2.5rem)     /* 24-40px */
```

### Шрифты
```css
--font-mono: 'VT323', 'Courier New', monospace
--font-pixel: 'Press Start 2P', 'VT323', monospace
```

---

## 🔧 КОНФИГУРАЦИЯ

### Vite (vite.config.js)
- **Base URL:** `/RETRO-PC-STORE/` (GitHub Pages)
- **Dev port:** 3000
- **Minification:** Terser
- **Plugins:** PWA, Legacy, Compression

### Package.json
- **Версия:** 3.3.0
- **Тип:** module (ES6)
- **Скрипты:** dev, build, preview, lint

### Manifest (manifest.json)
- **Название:** Retro-PC Store
- **Тема:** #33FF33 (зеленый)
- **Фон:** #0D0D0D (черный)
- **Display:** standalone

---

## 📈 МЕТРИКИ

### Текущее состояние
```
✅ Lighthouse Score: 95+
✅ LCP: < 1.2s
✅ FID: < 100ms
✅ CLS: < 0.1
✅ Accessibility: WCAG 2.1 AA
✅ Bundle Size: ~150KB
```

### Цели после рефакторинга
```
🎯 Lighthouse Score: 100/100
🎯 LCP: < 1.0s
🎯 Bundle Size: < 50KB (gzipped)
🎯 PWA Score: 100
🎯 Модульная архитектура
```

---

## 🔗 ПОЛЕЗНЫЕ ССЫЛКИ

### Документация технологий
- [Vite](https://vitejs.dev/)
- [Sass](https://sass-lang.com/)
- [PWA](https://web.dev/progressive-web-apps/)
- [Workbox](https://developers.google.com/web/tools/workbox)

### Инструменты
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [WebPageTest](https://www.webpagetest.org/)
- [Can I Use](https://caniuse.com/)

### Репозиторий
- **GitHub:** https://github.com/Tiger884/RETRO-PC-STORE
- **Live Demo:** https://tiger884.github.io/RETRO-PC-STORE/

---

## 🆘 ПОМОЩЬ

### Если что-то сломалось
```bash
# 1. Откатиться к последнему рабочему коммиту
git log --oneline        # Найти хороший коммит
git checkout <commit>    # Вернуться к нему

# 2. Очистить кеш
rm -rf node_modules dist
npm install
npm run dev

# 3. Проверить браузерную консоль
F12 → Console → Искать ошибки
```

### Куда обращаться
1. Проверить `docs/PROJECT_ARCHITECTURE_MAP.md` - там все детали
2. Прочитать `docs/REFACTORING_ROADMAP.md` - там примеры кода
3. Изучить `docs/DEVELOPMENT.md` - там про стили и оптимизацию

---

## ✅ ЧЕКЛИСТ ПЕРЕД КОММИТОМ

- [ ] Код работает в dev режиме (`npm run dev`)
- [ ] Код собирается без ошибок (`npm run build`)
- [ ] Нет ошибок в консоли браузера
- [ ] Все темы переключаются корректно
- [ ] Адаптивность работает (проверить на разных экранах)
- [ ] Accessibility не нарушена (Lighthouse Accessibility > 95)
- [ ] Обновлена документация (если нужно)

---

## 🎯 СЛЕДУЮЩИЕ ШАГИ

1. ✅ **Прочитали эту справку**
2. ⏸️ **Откройте PROJECT_ARCHITECTURE_MAP.md** - понять структуру
3. ⏸️ **Откройте REFACTORING_ROADMAP.md** - начать рефакторинг
4. ⏸️ **Создайте Git ветку** - изолировать изменения
5. ⏸️ **Начните с Фазы 1** - настройка инфраструктуры

---

**🚀 Вся информация для успешного рефакторинга у вас есть!**

*Обновлено: 14 октября 2025*
