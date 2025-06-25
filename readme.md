# Kurs języka norweskiego - Automatyczna publikacja

Ten projekt wykorzystuje GitHub Actions do automatycznego budowania i publikowania dokumentacji MkDocs na GitHub Pages.

## 🚀 Szybkie uruchomienie

### 1. Utwórz repozytorium na GitHub
```bash
# Utwórz nowe repozytorium na GitHub o nazwie "norwegian-course"
# Następnie sklonuj je lokalnie:
git clone https://github.com/TWOJA-NAZWA-UZYTKOWNIKA/norwegian-course.git
cd norwegian-course
```

### 2. Skopiuj pliki projektu
Skopiuj wszystkie pliki z projektu MkDocs do swojego lokalnego repozytorium:

```
norwegian-course/
├── .github/
│   └── workflows/
│       └── ci.yml                    # GitHub Actions workflow
├── docs/
│   ├── index.md                      # Strona główna
│   ├── lekcje/                       # Katalog z lekcjami
│   ├── gramatyka/                    # Materiały gramatyczne
│   └── cwiczenia/                    # Ćwiczenia
├── mkdocs.yml                        # Konfiguracja MkDocs
├── requirements.txt                  # Zależności Python
└── README.md                         # Ten plik
```

### 3. Skonfiguruj GitHub Pages
1. Przejdź do **Settings** → **Pages** w swoim repozytorium
2. W sekcji **Source** wybierz **GitHub Actions**
3. Zapisz ustawienia

### 4. Edytuj konfigurację
W pliku `mkdocs.yml` zmień:
```yaml
site_url: "https://TWOJA-NAZWA-UZYTKOWNIKA.github.io/norwegian-course/"
repo_url: "https://github.com/TWOJA-NAZWA-UZYTKOWNIKA/norwegian-course"
```

### 5. Wyślij zmiany
```bash
git add .
git commit -m "Initial commit - Norwegian course setup"
git push origin main
```

## 🔄 Jak działa automatyzacja

### Wyzwalacze pipeline'u:
- **Push do main/master** - automatyczne budowanie i publikacja
- **Pull Request** - tylko budowanie (bez publikacji)
- **Manualne uruchomienie** - możesz uruchomić przez GitHub Actions tab

### Co się dzieje automatycznie:
1. **Checkout kodu** - pobieranie najnowszej wersji
2. **Instalacja Pythona** - konfiguracja środowiska
3. **Cache zależności** - przyspieszenie kolejnych budowań
4. **Instalacja pakietów** - `pip install -r requirements.txt`
5. **Budowanie MkDocs** - `mkdocs build`
6. **Deploy na GitHub Pages** - automatyczna publikacja

## 🛠️ Rozwiązywanie problemów

### ❌ Build Errors - Naprawione!
Jeśli spotkałeś błędy typu:
- `mkdocs_material_extensions is deprecated`
- `search.lang 'pl' is not supported`
- `AttributeError: 'bool' object has no attribute 'split'`

✅ **Rozwiązanie**: Użyj **uproszczonej konfiguracji**:
- Skopiuj `mkdocs.yml - Uproszczona stabilna konfiguracja`
- Skopiuj `requirements.txt - Uproszczona wersja`

### Główne zmiany w naprawionej konfiguracji:
1. **Usunięto przestarzałe pakiety** (`mkdocs-material-extensions`)
2. **Naprawiono konfigurację search** (tylko `lang: en`)
3. **Uproszczono emoji extensions** (kompatybilne API)
4. **Usunięto problematyczne pluginy** (awesome-pages)

## 📚 Struktura dokumentacji

### Lekcje (1-22)
- Kompletny kurs od podstaw do zaawansowanego poziomu
- Każda lekcja zawiera teorię, przykłady i ćwiczenia

### Gramatyka
- Stopniowanie przymiotników
- Zaimki osobowe i dzierżawcze
- Czasowniki nieregularne
- Czasy przeszłe

### Ćwiczenia interaktywne
- Praktyczne zadania do każdej lekcji
- Odpowiedzi i wyjaśnienia
- Dialogi sytuacyjne

## 🔧 Lokalne uruchamianie

Jeśli chcesz pracować lokalnie:

```bash
# Instalacja zależności
pip install -r requirements.txt

# Uruchomienie serwera deweloperskiego
mkdocs serve

# Dokumentacja będzie dostępna pod: http://127.0.0.1:8000
```

## 🎯 Dodawanie nowych treści

1. **Nowa lekcja**:
   ```bash
   # Utwórz plik w docs/lekcje/
   docs/lekcje/lekcja-XX.md
   ```

2. **Dodaj do nawigacji** w `mkdocs.yml`:
   ```yaml
   nav:
     - "Lekcja XX": lekcje/lekcja-XX.md
   ```

3. **Wyślij zmiany**:
   ```bash
   git add .
   git commit -m "Add lesson XX"
   git push
   ```

Pipeline automatycznie zbuduje i opublikuje zmiany!

## 📞 Jeśli nadal masz problemy:

1. **Sprawdź Actions tab** w GitHub - tam znajdziesz szczegółowe logi
2. **Używaj uproszczonej konfiguracji** - zawsze działa
3. **Sprawdź składnię YAML** w `mkdocs.yml`
4. **Upewnij się o poprawnych ścieżkach** do plików

---

**Powodzenia z kursem norweskiego!** 🇳🇴

*Lykke til med læringen!*
