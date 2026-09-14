# LangJS 

[![npm version](https://img.shields.io/npm/v/langjs.js)](https://www.npmjs.com/package/langjs.js)
[![NPM Downloads](https://img.shields.io/npm/dm/langjs.js)](https://www.npmjs.com/package/langjs.js)
[![NPM License](https://img.shields.io/npm/l/langjs.js)](https://www.npmjs.com/package/langjs.js)

A simple yet powerful JavaScript framework for multilingual translation management on your web pages. Dependency-free, lightweight, and easy to use.

## ✨ Features

- ✅ **Vanilla JavaScript** - No dependencies required
- 🚀 **Lightweight & Fast** - < 10KB minified
- 🔄 **Auto-Detection** - Detects browser language automatically
- 💾 **Persistence** - Saves user language preferences
- 🎯 **Dot Notation** - Supports nested keys (`home.title.main`)
- 🔍 **DOM Observation** - Automatically translates dynamic content
- 🎨 **Interpolation** - Supports parameters within translations
- 📅 **Formatting** - Format dates, numbers, and currencies
- 🌐 **RTL Support** - Supports right-to-left languages
- ⚡ **Smart Cache** - Optimized performance

## 📦 Installation

### Option 1: Direct Download

```html
<script src="path/to/langjs.js"></script>
```

### Option 2: npm
```bash
npm install langjs.js
```


## 🚀 Quick Start

### 1. File Structure

```
votre-projet/
├── index.html
├── js/
│   └── langjs.js
└── lang/
    ├── en.json
    └── fr.json
```

### 2. Create Language Files

**lang/en.json**
```json
{
  "home": {
    "title": "Welcome to LangJS",
    "subtitle": "Easy multilingual management",
    "description": "Translate your website in seconds!"
  },
  "nav": {
    "home": "Home",
    "about": "About",
    "contact": "Contact"
  },
  "form": {
    "name": "Name",
    "email": "Email",
    "submit": "Send"
  }
}
```

**lang/fr.json**
```json
{
  "home": {
    "title": "Bienvenue sur LangJS",
    "subtitle": "Gestion multilingue facile",
    "description": "Traduisez votre site en quelques secondes !"
  },
  "nav": {
    "home": "Accueil",
    "about": "À propos",
    "contact": "Contact"
  },
  "form": {
    "name": "Nom",
    "email": "Email",
    "submit": "Envoyer"
  }
}
```

### 3. Basic HTML Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>LangJS Demo</title>
  <script src="js/langjs.js"></script>
</head>
<body>
  
  <!-- Automatic translation using the translate attribute -->
  <h1 translate="home.title"></h1>
  <p translate="home.description"></p>

  <!-- Language Selector -->
  <select id="langSelector">
    <option value="en">English</option>
    <option value="fr">Français</option>
  </select>

  <script>
    // Simple Initialization
    const lang = new LangJS({
      availableLanguages: ['en', 'fr'],
      defaultLanguage: 'en'
    });

    // Language Change Event
    document.getElementById('langSelector').addEventListener('change', (e) => {
      lang.setLanguage(e.target.value);
    });
  </script>
</body>
</html>
```

## 📖 Advanced Configuration

### Configuration Options

```javascript
const lang = new LangJS({
  // Path to JSON files
  languagePath: './lang/',
  
  // Default language
  defaultLanguage: 'en',
  
  // Fallback language if a translation is missing
  fallbackLanguage: 'en',
  
  // Available languages
  availableLanguages: ['en', 'fr', 'es', 'de'],
  
  // localStorage storage key
  persistKey: 'langjs_language',
  
  // Detect browser language
  detectBrowser: true,
  
  // Automatic initialization
  autoInit: true,
  
  // Custom HTML attributes
  attributes: ['translate', 'data-translate', 'data-i18n'],
  
  // Attribute for placeholders
  placeholderAttribute: 'translate-placeholder',
  
  // Attribute for titles (tooltips)
  titleAttribute: 'translate-title',
  
  // Callback triggered when the language changes
  onLanguageChange: (newLang) => {
    console.log('Language changed to:', newLang);
  },
  
  // Debug mode
  debug: true
});
```

## 💡 Usage

### Text Translation

```html
<!-- translate attribute -->
<h1 translate="home.title"></h1>

<!-- data-translate attribute -->
<p data-translate="home.description"></p>

<!-- Placeholder translation -->
<input type="text" translate-placeholder="form.name">

<!-- Title translation (tooltip) -->
<button translate-title="form.submit">🚀</button>

<!-- Aria-label translation for accessibility -->
<button translate-aria="nav.close">X</button>
```

### JavaScript Translation

```javascript
// Simple translation
const title = lang.get('home.title');

// Translation with parameters
const welcome = lang.get('welcome.message', { name: 'John' });
// If welcome.message = "Hello {name}!" => "Hello John!"

// Translate a specific element
const element = document.getElementById('myElement');
lang.translateElement(element);
```

### Switching Languages

```javascript
// Asynchronous method
await lang.setLanguage('fr');

// Get the current language
const current = lang.getCurrentLanguage(); // 'fr'

// Check if a language is available
if (lang.isLanguageAvailable('es')) {
  lang.setLanguage('es');
}

// Get all available languages
const languages = lang.getAvailableLanguages(); // ['en', 'fr']
```

### Formatting

```javascript
// Format a number
lang.formatNumber(1234567.89); 
// en: "1,234,567.89"
// fr: "1 234 567,89"

// Format a date
lang.formatDate(new Date(), { 
  year: 'numeric', 
  month: 'long', 
  day: 'numeric' 
});
// en: "November 8, 2025"
// fr: "8 novembre 2025"

// Format a currency
lang.formatCurrency(99.99, 'USD');
// en: "$99.99"
// fr: "99,99 $US"

lang.formatCurrency(49.99, 'EUR');
// en: "€49.99"
// fr: "49,99 €"
```

### RTL Support

```javascript
// Get the text direction of the language
const direction = lang.getLanguageDirection(); // 'ltr' or 'rtl'

// Automatically apply text direction to the document
lang.applyDirection(); // Adds dir="rtl" or dir="ltr" to the <html> tag
```

## 🎯 Implementation Examples

### Example 1: Simple Website

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Website</title>
  <script src="js/langjs.js"></script>
</head>
<body>
  <nav>
    <a translate="nav.home"></a>
    <a translate="nav.about"></a>
    <select id="lang">
      <option value="en">🇬🇧 English</option>
      <option value="fr">🇫🇷 Français</option>
    </select>
  </nav>

  <main>
    <h1 translate="page.title"></h1>
    <p translate="page.content"></p>
  </main>

  <script>
    const lang = new LangJS();
    
    document.getElementById('lang').addEventListener('change', (e) => {
      lang.setLanguage(e.target.value);
    });
  </script>
</body>
</html>
```

### Example 2: Form with Validation

```html
<form id="contactForm">
  <input type="text" 
         translate-placeholder="form.name" 
         required>
  
  <input type="email" 
         translate-placeholder="form.email" 
         required>
  
  <button type="submit" translate="form.submit"></button>
  
  <span id="error" translate="form.error" style="display:none;"></span>
</form>

<script>
  const lang = new LangJS({
    onLanguageChange: (newLang) => {
      // Revalidate the form with the updated language messages
      validateForm();
    }
  });
</script>
```

### Example 3: Dynamic Content

```javascript
// Dynamically added content is automatically translated
function addMessage(key) {
  const div = document.createElement('div');
  div.setAttribute('translate', key);
  document.body.appendChild(div);
  // LangJS automatically detects and translates the new element
}

addMessage('notifications.success');
```

### Example 4: Translations with Parameters

**lang/en.json**
```json
{
  "welcome": "Welcome {name}!",
  "items": "You have {count} item(s)",
  "email": "Sent to {email} on {date}"
}
```

```javascript
lang.get('welcome', { name: 'Marie' });
// "Welcome Marie!"

lang.get('items', { count: 5 });
// "You have 5 item(s)"

lang.get('email', { 
  email: 'test@example.com',
  date: '08/11/2025'
});
// "Sent to test@example.com on 08/11/2025"
```

## 🎨 Framework Integration

### With React

```javascript
import { useState, useEffect, useRef } from 'react';
import LangJS from './langjs';

function App() {
  const [language, setLanguage] = useState('en');
  const langRef = useRef(null);

  useEffect(() => {
    langRef.current = new LangJS({
      availableLanguages: ['en', 'fr'],
      onLanguageChange: (newLang) => setLanguage(newLang)
    });
  }, []);

  const changeLanguage = (lang) => {
    langRef.current.setLanguage(lang);
  };

  return (
    <div>
      <h1 translate="app.title"></h1>
      <button onClick={() => changeLanguage('fr')}>FR</button>
    </div>
  );
}
```

### With Vue.js

```javascript
import LangJS from './langjs';

export default {
  data() {
    return {
      lang: null
    }
  },
  mounted() {
    this.lang = new LangJS({
      availableLanguages: ['en', 'fr']
    });
  },
  methods: {
    changeLanguage(newLang) {
      this.lang.setLanguage(newLang);
    }
  }
}
```

## 🔧 Full API

### Core Methods

| Method | Description |
|---------|-------------|
| `setLanguage(lang)` | Changes the active language (async) |
| `get(key, params)` | Retrieves a translation string |
| `getCurrentLanguage()` | Returns the active language |
| `getAvailableLanguages()` | Lists all configured languages |
| `translatePage()` | Translates the entire DOM |
| `translateElement(el)` | Translates a specific DOM element |
| `formatNumber(num, opts)` | Formats a number based on locale |
| `formatDate(date, opts)` | Formates a date based on locale |
| `formatCurrency(amount, currency)` | Formats a currency value |
| `getLanguageDirection()` | Returns text direction ('ltr' or 'rtl') |
| `applyDirection()` | Applies text direction to the html element |
| `destroy()` | Cleans up the instance and observers |

## 🐛 Troubleshooting

### Translations are not showing up

1. Verify that your JSON files are located in the correct directory.
2. Open your browser console to check for loading or execution errors.
3. Enable debug mode in your configuration: `debug: true`.

### Language settings do not persist

Make sure that `localStorage` is accessible in your web browser (it might be disabled or restricted in private browsing/incognito mode).

### Dynamic elements are not being translated

LangJS automatically monitors the DOM, but you can manually force an update on a specific node:
```javascript
lang.translateElement(myElement);
```

## 📄 License

MIT License - Free to use for both personal and commercial projects.

## 👨‍💻 Author

Developed by [Emmadiblo257](https://github.com/emmadiblo257)

## 🤝 Contributing

Contributions are always welcome! Feel free to open an issue or submit a pull request on the official repository.

*Enjoy coding! 🚀*
