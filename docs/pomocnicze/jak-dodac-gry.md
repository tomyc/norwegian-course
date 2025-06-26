# Jak dodać interaktywne gry do MkDocs

## 🎯 Dostępne metody

### Metoda 1: Osobne pliki HTML ⭐ **ZALECANA**

**Zalety:**
- ✅ Pełna kontrola nad kodem
- ✅ Szybkie ładowanie
- ✅ Łatwa konserwacja
- ✅ Możliwość osobnych stylów CSS

**Kroki:**
1. Utwórz folder `docs/games/`
2. Skopiuj plik `memory_game.html` → `docs/games/memory-game.html`
3. Dodaj link w nawigacji MkDocs
4. Linkuj bezpośrednio: `[Memory Game](../games/memory-game.html)`

### Metoda 2: HTML wewnątrz Markdown

**Dla mniejszych interaktywnych elementów:**

```markdown
# Moja strona z grą

<div id="quiz-container">
    <style>
        #quiz-container { background: #f0f0f0; padding: 20px; }
        .question { font-weight: bold; }
    </style>
    
    <div class="question">Jak się mówi "cześć" po norwesku?</div>
    <button onclick="checkAnswer('hei')">hei</button>
    <button onclick="checkAnswer('takk')">takk</button>
    
    <script>
        function checkAnswer(answer) {
            if (answer === 'hei') {
                alert('Poprawnie! 🎉');
            } else {
                alert('Spróbuj ponownie!');
            }
        }
    </script>
</div>
```

### Metoda 3: Iframe dla zewnętrznych gier

```markdown
# Embedded Game

<iframe src="../games/memory-game.html" 
        width="100%" 
        height="800px" 
        style="border: none; border-radius: 10px;">
</iframe>
```

## 📁 Zalecana struktura folderów

```
docs/
├── games/                     # Wszystkie gry
│   ├── index.md              # Przegląd gier
│   ├── memory-game.html      # Memory Game
│   ├── pronunciation-trainer.html
│   ├── quiz-generator.html
│   └── assets/               # Wspólne zasoby
│       ├── css/
│       ├── js/
│       └── images/
├── cwiczenia/                # Ćwiczenia tekstowe
├── lekcje-podstawowe/
└── ...
```

## ⚙️ Konfiguracja MkDocs

**Dodaj do `mkdocs.yml`:**

```yaml
nav:
  - Strona główna: index.md
  - # ... inne sekcje
  - 🎮 Gry i ćwiczenia:
    - Przegląd gier: games/index.md
    - Memory Game: games/memory-game.html
    - Pronunciation Trainer: games/pronunciation_trainer.html
    - Quiz Generator: games/quiz-generator.html
```

## 🔧 Wskazówki techniczne

### 1. Responsive Design
```css
/* W swoich grach używaj responsywnego CSS */
@media (max-width: 768px) {
    .game-board {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

### 2. Preloadowanie zasobów
```html
<!-- Na początku HTML -->
<link rel="preload" href="assets/css/game.css" as="style">
<link rel="preload" href="assets/js/game.js" as="script">
```

### 3. Lokalne fonty i ikony
```css
/* Używaj lokalnych fontów */
@font-face {
    font-family: 'GameFont';
    src: url('../assets/fonts/game-font.woff2') format('woff2');
}
```

### 4. Optymalizacja dla MkDocs
```html
<!-- Na początku każdego pliku gry -->
<base href="." />
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 🎨 Style spójne z motywem Material

```css
/* Kolory zgodne z motywem Material */
:root {
    --primary-color: #1976d2;      /* MkDocs Material primary */
    --accent-color: #ff5722;       /* MkDocs Material accent */
    --background: #fafafa;
    --surface: #ffffff;
    --text-primary: #212121;
    --text-secondary: #757575;
}

.game-container {
    background: var(--surface);
    color: var(--text-primary);
    border: 1px solid #e0e0e0;
    border-radius: 4px;     /* Material Design border radius */
}
```

## 📊 Integracja z Progress Tracking

```javascript
// Zapisywanie postępów w localStorage
function saveProgress(gameType, score, level) {
    const progress = JSON.parse(localStorage.getItem('norwegian-progress') || '{}');
    if (!progress.games) progress.games = {};
    
    progress.games[gameType] = {
        bestScore: Math.max(progress.games[gameType]?.bestScore || 0, score),
        level: level,
        completedAt: new Date().toISOString()
    };
    
    localStorage.setItem('norwegian-progress', JSON.stringify(progress));
}

// Odczytywanie postępów
function loadProgress(gameType) {
    const progress = JSON.parse(localStorage.getItem('norwegian-progress') || '{}');
    return progress.games?.[gameType] || { bestScore: 0, level: 1 };
}
```

## 🚀 Deployment

### Przy lokalnym buildu:
```bash
cd /Users/tomasz/PycharmProjects/norwegian-course
mkdocs serve    # Test lokalny
mkdocs build    # Build do folderu site/
```

### Weryfikacja:
- ✅ Sprawdź czy pliki `.html` są w `site/games/`
- ✅ Czy linki działają poprawnie
- ✅ Czy gry ładują się bez błędów konsoli

## 📱 Mobilna optymalizacja

```css
/* Touch-friendly buttons */
.game-button {
    min-height: 44px;    /* iOS guideline */
    min-width: 44px;
    touch-action: manipulation;
}

/* Prevent zoom on input focus */
input, select, textarea {
    font-size: 16px;     /* Prevents iOS zoom */
}
```

## 🎯 Przykład integracji

**Link do gry na stronie lekcji:**

```markdown
# Lekcja 11: Jedzenie

## Ćwiczenia praktyczne

Po przeczytaniu lekcji, przetestuj swoją wiedzę:

🎮 **[Zagraj w Memory Game - Jedzenie](../games/memory-game.html?category=food)**

🔊 **[Ćwicz wymowę słów z jedzeniem](../games/pronunciation_trainer.html?category=food)**
```

## ⚡ Optimalizacje wydajności

```html
<!-- Lazy loading dla obrazków -->
<img src="placeholder.jpg" data-src="actual-image.jpg" loading="lazy">

<!-- Preconnect dla zewnętrznych CDN -->
<link rel="preconnect" href="https://fonts.googleapis.com">

<!-- Service Worker dla offline -->
<script>
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
}
</script>
```

---

## ✅ Podsumowanie

**Najlepsza praktyka:**
1. Użyj **Metody 1** (osobne pliki HTML)
2. Umieść w folderze `docs/games/`
3. Dodaj do nawigacji MkDocs
4. Używaj spójnego designu z motywem Material
5. Optymalizuj dla urządzeń mobilnych

**Twoja gra Memory Game jest gotowa do integracji!** 🎉
