# 📚 Динамическая Wiki-система v3.3.2

## ✅ Реализовано

### Архитектура

- **Разделение контента и представления**: контент в `.txt` файлах, логика в JavaScript
- **Динамическая загрузка**: Fetch API + async/await
- **Парсер текста в HTML**: поддержка заголовков, списков, таблиц

### Структура проекта

```plaintext
wiki-content/
├── processors.txt   (40 строк) - Процессоры Intel 8086/8088/8087/80286
├── computers.txt    (35 строк) - IBM PC/XT/AT
├── history.txt      (18 строк) - Хронология и факты
└── tech.txt         (30 строк) - Техническая информация

assets/js/
└── wiki-loader.js   (130+ строк) - Система загрузки
```

## 🚀 Как это работает

### 1. Формат .txt файлов

```txt
# Заголовок раздела
Обычный текст параграфа.

## Подзаголовок
- Элемент списка 1
- Элемент списка 2

**Жирный текст:** значение
---
Разделитель секций

| Колонка1 | Колонка2 |
| Данные1  | Данные2  |
```

### 2. Парсер WikiLoader.parseContent()

Поддерживаемые форматы:

- `#` → `<h3>` заголовок
- `##` → `<h4>` подзаголовок  
- `**текст:**` → `<strong>текст:</strong>` ключ-значение
- `- элемент` → `<li>` элемент списка
- `---` → разделитель карточек
- `| col1 | col2 |` → таблицы HTML

### 3. Загрузка контента

```javascript
// При открытии Wiki автоматически загружается весь контент
window.WikiLoader.loadAllSections();

// Загрузка одной секции
await WikiLoader.loadSection('processors');
// → fetch('wiki-content/processors.txt')
// → parseContent(text) 
// → вставка HTML в #wiki-processors
```

## 📝 Добавление нового контента

### Шаг 1: Создайте .txt файл

```bash
# В папке wiki-content/
echo "# Новый раздел" > new-section.txt
```

### Шаг 2: Зарегистрируйте в wiki-loader.js

```javascript
contentFiles: {
    'wiki-processors': 'wiki-content/processors.txt',
    'wiki-computers': 'wiki-content/computers.txt',
    'wiki-history': 'wiki-content/history.txt',
    'wiki-tech': 'wiki-content/tech.txt',
    'wiki-newsection': 'wiki-content/new-section.txt'  // ← добавить
}
```

### Шаг 3: Добавьте секцию в index.html

```html
<div id="wiki-newsection" class="wiki-section">
    <p class="loading">⏳ Загрузка контента...</p>
</div>
```

### Шаг 4: Добавьте кнопку вкладки

```html
<button class="wiki-tab" onclick="switchWikiTab('wiki-newsection')">
    📄 Новый раздел
</button>
```

## 🎯 Преимущества

### Для разработчика

- ✅ Контент отдельно от кода (легче редактировать)
- ✅ Простой формат .txt (не нужен HTML)
- ✅ Git-friendly (видны diff при изменениях)
- ✅ Переиспользуемый код (WikiLoader)

### Для производительности

- ✅ Асинхронная загрузка (не блокирует UI)
- ✅ Загрузка только при открытии Wiki
- ✅ Кеширование браузера (.txt файлы)
- ✅ Меньший размер index.html (207 строк вместо 441)

### Для пользователя

- ✅ Индикатор загрузки "⏳ Загрузка контента..."
- ✅ Обработка ошибок (если файл не загрузился)
- ✅ Безопасный HTML (escapeHtml для пользовательского контента)

## 🔧 Техническая реализация

### wiki-loader.js

```javascript
window.WikiLoader = {
    // Карта: ID секции → путь к .txt файлу
    contentFiles: {
        'wiki-processors': 'wiki-content/processors.txt',
        // ...
    },

    // Загрузка одной секции
    loadSection: async function(sectionId) {
        const path = this.contentFiles[sectionId];
        const response = await fetch(path);
        if (!response.ok) throw new Error(`HTTP ${response.status}`);
        const text = await response.text();
        const html = this.parseContent(text);
        document.getElementById(sectionId).innerHTML = html;
    },

    // Парсер .txt → HTML
    parseContent: function(text) {
        // Разбивка на карточки по "---"
        // Преобразование разметки в HTML
        // Возврат готового HTML
    },

    // Загрузка всех секций
    loadAllSections: async function() {
        for (let sectionId in this.contentFiles) {
            await this.loadSection(sectionId);
        }
    }
};

// Обёртка для showWiki() - загрузка при открытии
const originalShowWiki = window.showWiki;
window.showWiki = function() {
    originalShowWiki();
    WikiLoader.loadAllSections();
};
```

## 📊 Статистика

- **До оптимизации**: 441 строка в index.html (с хардкодом)
- **После оптимизации**: 207 строк в index.html (-53%)
- **Размер .txt файлов**: ~2 KB (4 файла)
- **Размер wiki-loader.js**: ~4 KB
- **Общий выигрыш**: Меньше дублирования, проще поддержка

## 🧪 Тестирование

### Ручное тестирование

1. Откройте `index.html` в браузере
2. Нажмите кнопку [ВИКИ]
3. Проверьте загрузку всех 4 секций:
   - 🖥️ Процессоры
   - 💾 Компьютеры
   - 📅 История
   - ⚙️ Технологии
4. Переключайтесь между вкладками (должны отображаться данные)

### Проверка в DevTools

```javascript
// Консоль браузера
console.log(WikiLoader.contentFiles);
// → {wiki-processors: "wiki-content/processors.txt", ...}

await WikiLoader.loadSection('wiki-processors');
// → Секция должна загрузиться без ошибок
```

## 🐛 Отладка

### Проблема: "Загрузка контента..." не исчезает

**Причина**: Ошибка fetch (404, CORS)  
**Решение**: Откройте DevTools → Console, проверьте ошибки сети

### Проблема: Текст отображается криво

**Причина**: Неверный формат .txt файла  
**Решение**: Проверьте разметку (заголовки, списки, таблицы)

### Проблема: Вкладки не переключаются

**Причина**: Конфликт с main.js  
**Решение**: Убедитесь что wiki-loader.js загружается ПЕРЕД main.js

## 📋 TODO

- [ ] Добавить прогресс-бар загрузки
- [ ] Кеширование в localStorage (оффлайн режим)
- [ ] Поддержка Markdown (опционально)
- [ ] Версионирование контента (.txt с версиями)
- [ ] Админка для редактирования .txt файлов

## 📦 Версия

**v3.3.2** - Динамическая Wiki-система (21.01.2025)

---

**Документ создан**: 21.01.2025  
**Автор**: GitHub Copilot  
**Статус**: ✅ Готово к использованию
