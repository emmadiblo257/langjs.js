# LangJS v2.0 🌍

Un framework JavaScript moderne et puissant pour la gestion multilingue de vos pages web. Sans dépendances, léger et facile à utiliser.

## ✨ Fonctionnalités

- ✅ **Vanilla JavaScript** - Aucune dépendance requise
- 🚀 **Léger et rapide** - < 5KB minifié
- 🔄 **Détection automatique** - Langue du navigateur
- 💾 **Persistance** - Sauvegarde de la préférence utilisateur
- 🎯 **Notation par points** - Clés imbriquées (`home.title.main`)
- 🔍 **Observation DOM** - Traduction automatique du contenu dynamique
- 🎨 **Interpolation** - Paramètres dans les traductions
- 📅 **Formatage** - Dates, nombres et devises
- 🌐 **RTL Support** - Langues de droite à gauche
- ⚡ **Cache intelligent** - Performance optimisée

## 📦 Installation

### Option 1: Téléchargement direct

```html
<script src="path/to/langjs.js"></script>
```

### Option 2: CDN (à venir)

```html
<script src="https://cdn.jsdelivr.net/npm/langjs@2.0.0/dist/langjs.min.js"></script>
```

## 🚀 Démarrage rapide

### 1. Structure des fichiers

```
votre-projet/
├── index.html
├── js/
│   └── langjs.js
└── lang/
    ├── en.json
    └── fr.json
```

### 2. Créer les fichiers de langue

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

### 3. HTML de base

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>LangJS Demo</title>
  <script src="js/langjs.js"></script>
</head>
<body>
  
  <!-- Traduction automatique avec l'attribut translate -->
  <h1 translate="home.title"></h1>
  <p translate="home.description"></p>

  <!-- Sélecteur de langue -->
  <select id="langSelector">
    <option value="en">English</option>
    <option value="fr">Français</option>
  </select>

  <script>
    // Initialisation simple
    const lang = new LangJS({
      availableLanguages: ['en', 'fr'],
      defaultLanguage: 'en'
    });

    // Changement de langue
    document.getElementById('langSelector').addEventListener('change', (e) => {
      lang.setLanguage(e.target.value);
    });
  </script>
</body>
</html>
```

## 📖 Configuration avancée

### Options de configuration

```javascript
const lang = new LangJS({
  // Chemin vers les fichiers JSON
  languagePath: './lang/',
  
  // Langue par défaut
  defaultLanguage: 'en',
  
  // Langue de secours si une traduction manque
  fallbackLanguage: 'en',
  
  // Langues disponibles
  availableLanguages: ['en', 'fr', 'es', 'de'],
  
  // Clé de stockage localStorage
  persistKey: 'langjs_language',
  
  // Détecter la langue du navigateur
  detectBrowser: true,
  
  // Initialisation automatique
  autoInit: true,
  
  // Attributs HTML personnalisés
  attributes: ['translate', 'data-translate', 'data-i18n'],
  
  // Attribut pour les placeholders
  placeholderAttribute: 'translate-placeholder',
  
  // Attribut pour les titres (tooltips)
  titleAttribute: 'translate-title',
  
  // Callback quand la langue change
  onLanguageChange: (newLang) => {
    console.log('Langue changée:', newLang);
  },
  
  // Mode debug
  debug: true
});
```

## 💡 Utilisation

### Traduction de texte

```html
<!-- Attribut translate -->
<h1 translate="home.title"></h1>

<!-- Attribut data-translate -->
<p data-translate="home.description"></p>

<!-- Placeholder -->
<input type="text" translate-placeholder="form.name">

<!-- Title (tooltip) -->
<button translate-title="form.submit">🚀</button>

<!-- Aria-label pour l'accessibilité -->
<button translate-aria="nav.close">X</button>
```

### Traduction en JavaScript

```javascript
// Traduction simple
const title = lang.get('home.title');

// Traduction avec paramètres
const welcome = lang.get('welcome.message', { name: 'John' });
// Si welcome.message = "Hello {name}!" => "Hello John!"

// Traduction d'un élément spécifique
const element = document.getElementById('myElement');
lang.translateElement(element);
```

### Changer de langue

```javascript
// Méthode asynchrone
await lang.setLanguage('fr');

// Obtenir la langue actuelle
const current = lang.getCurrentLanguage(); // 'fr'

// Vérifier si une langue est disponible
if (lang.isLanguageAvailable('es')) {
  lang.setLanguage('es');
}

// Obtenir toutes les langues disponibles
const languages = lang.getAvailableLanguages(); // ['en', 'fr']
```

### Formatage

```javascript
// Formater un nombre
lang.formatNumber(1234567.89); 
// en: "1,234,567.89"
// fr: "1 234 567,89"

// Formater une date
lang.formatDate(new Date(), { 
  year: 'numeric', 
  month: 'long', 
  day: 'numeric' 
});
// en: "November 8, 2025"
// fr: "8 novembre 2025"

// Formater une devise
lang.formatCurrency(99.99, 'USD');
// en: "$99.99"
// fr: "99,99 $US"

lang.formatCurrency(49.99, 'EUR');
// en: "€49.99"
// fr: "49,99 €"
```

### Support RTL

```javascript
// Obtenir la direction de la langue
const direction = lang.getLanguageDirection(); // 'ltr' ou 'rtl'

// Appliquer automatiquement la direction au document
lang.applyDirection(); // Ajoute dir="rtl" ou dir="ltr" au <html>
```

## 🎯 Exemples d'utilisation

### Exemple 1: Site web simple

```html
<!DOCTYPE html>
<html>
<head>
  <title>Mon Site</title>
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

### Exemple 2: Formulaire avec validation

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
      // Revalider le formulaire avec les nouveaux messages
      validateForm();
    }
  });
</script>
```

### Exemple 3: Contenu dynamique

```javascript
// Le contenu ajouté dynamiquement est automatiquement traduit
function addMessage(key) {
  const div = document.createElement('div');
  div.setAttribute('translate', key);
  document.body.appendChild(div);
  // LangJS détecte et traduit automatiquement le nouvel élément
}

addMessage('notifications.success');
```

### Exemple 4: Traduction avec paramètres

**lang/fr.json**
```json
{
  "welcome": "Bienvenue {name} !",
  "items": "Vous avez {count} article(s)",
  "email": "Envoyé à {email} le {date}"
}
```

```javascript
lang.get('welcome', { name: 'Marie' });
// "Bienvenue Marie !"

lang.get('items', { count: 5 });
// "Vous avez 5 article(s)"

lang.get('email', { 
  email: 'test@example.com',
  date: '08/11/2025'
});
// "Envoyé à test@example.com le 08/11/2025"
```

## 🎨 Intégration avec des frameworks

### Avec React

```javascript
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

### Avec Vue.js

```javascript
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

## 🔧 API Complète

### Méthodes principales

| Méthode | Description |
|---------|-------------|
| `setLanguage(lang)` | Change la langue (async) |
| `get(key, params)` | Obtient une traduction |
| `getCurrentLanguage()` | Retourne la langue actuelle |
| `getAvailableLanguages()` | Liste les langues disponibles |
| `translatePage()` | Traduit toute la page |
| `translateElement(el)` | Traduit un élément spécifique |
| `formatNumber(num, opts)` | Formate un nombre |
| `formatDate(date, opts)` | Formate une date |
| `formatCurrency(amount, currency)` | Formate une devise |
| `getLanguageDirection()` | Retourne 'ltr' ou 'rtl' |
| `applyDirection()` | Applique la direction au document |
| `destroy()` | Nettoie l'instance |

## 🐛 Dépannage

### Les traductions ne s'affichent pas

1. Vérifiez que les fichiers JSON sont au bon endroit
2. Vérifiez la console pour les erreurs
3. Activez le mode debug: `debug: true`

### La langue ne persiste pas

Vérifiez que localStorage est disponible dans votre navigateur (peut être désactivé en navigation privée).

### Les éléments dynamiques ne sont pas traduits

LangJS observe automatiquement le DOM, mais vous pouvez forcer la traduction:
```javascript
lang.translateElement(monElement);
```

## 📄 Licence

MIT License - Libre d'utilisation dans vos projets personnels et commerciaux.

## 👨‍💻 Auteur

Développé par **Emmadiblo**

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou une pull request.

---

**Enjoy coding! 🚀**