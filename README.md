# 🇮🇩 → 🇺🇸 Indonesian Word Translator

A Chrome extension that displays inline English translations beneath every Indonesian word on news articles, helping language learners read native content without context-switching to a dictionary.

```
Presiden    mengumumkan   kebijakan   baru
President   announce      policy      new
```

---

## ✨ Features

- **Word-by-word annotations** — English translations appear directly below each Indonesian word, preserving the original reading flow (inspired by Japanese furigana)
- **Smart proper noun detection** — Names like "Prabowo" or "Jakarta" are left untouched, not mistranslated
- **Hybrid translation engine** — Combines a hand-curated 250+ word dictionary with the MyMemory translation API for accuracy that single-word machine translation can't match
- **Persistent caching** — Revisited pages translate instantly with no API calls
- **15+ supported Indonesian news sites** out of the box
- **Toggle on/off** with a single click via the popup
- **Dark mode support**

## 🌐 Supported Sites

The extension automatically activates on:

`kompas.com` · `detik.com` · `tribunnews.com` · `liputan6.com` · `tempo.co` · `cnnindonesia.com` · `antaranews.com` · `okezone.com` · `merdeka.com` · `suara.com` · `bisnis.com` · `republika.co.id` · `kumparan.com` · `tirto.id` · `medcom.id`

## 📦 Installation

### Option 1: From source (Developer mode)

1. Download or clone this repository
2. Open Chrome and navigate to `chrome://extensions/`
3. Enable **Developer mode** (toggle in the top-right corner)
4. Click **Load unpacked** and select the project folder
5. Pin the extension via the puzzle-piece icon for quick access

### Option 2: From the Chrome Web Store

*Coming soon*

## 🚀 Usage

1. Navigate to any supported Indonesian news site
2. Click the extension icon in your Chrome toolbar
3. Toggle translations **on**
4. The page will display English translations beneath each Indonesian word

To remove the annotations, simply toggle the extension **off**.

## 🏗️ How It Works

The extension uses a layered translation strategy to balance accuracy and performance:

```
┌─────────────────────────────────────────────────────┐
│  1. DOM Traversal: locate article content via       │
│     TreeWalker, skipping nav, ads, scripts          │
└─────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────┐
│  2. Tokenization: split text into words + separators│
└─────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────┐
│  3. Proper Noun Filter: skip capitalized mid-       │
│     sentence words and known names/places           │
└─────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────┐
│  4. Local Dictionary Lookup (250+ words)            │
│     Catches common particles, pronouns, news verbs  │
└─────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────┐
│  5. MyMemory API (only for words not in dictionary) │
│     Cached in chrome.storage for future visits      │
└─────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────┐
│  6. DOM Annotation: wrap each word in a styled span │
│     with the translation rendered beneath           │
└─────────────────────────────────────────────────────┘
```

## 📁 Project Structure

```
indonesian-translator-extension/
├── manifest.json       # Extension config and site permissions
├── content.js          # Main translation logic, DOM manipulation
├── styles.css          # Annotation styling
├── popup.html          # Toggle UI
├── popup.js            # Popup state management
└── icons/
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

## 🛠️ Tech Stack

- **JavaScript** (vanilla, no build step)
- **Chrome Extension Manifest V3**
- **Chrome Storage API** for persistent caching
- **MyMemory Translation API** for word lookups
- **HTML + CSS** for the popup UI

## 🧠 Adding to the Dictionary

To improve translation accuracy for a specific word, edit the `LOCAL_DICT` object in `content.js`:

```javascript
const LOCAL_DICT = {
  'word': 'translation',
  // ...
};
```

Reload the extension at `chrome://extensions/` to apply changes.

## 🗺️ Roadmap

- [ ] Publish to the Chrome Web Store
- [ ] Hover tooltips with multiple meanings for ambiguous words
- [ ] Click-to-save vocabulary list for review
- [ ] Support for additional Southeast Asian languages
- [ ] Offline-only mode using a bundled larger dictionary
- [ ] Optional context-aware sentence translation as fallback

## 🤝 Contributing

Found a mistranslation? Open an issue with:
- The Indonesian word
- The wrong translation it produced
- The correct translation

Pull requests welcome — particularly for expanding the local dictionary or adding new Indonesian news site selectors.

## 📄 License

MIT

## 🙏 Acknowledgments

- Translation backend powered by [MyMemory](https://mymemory.translated.net/)
- Inspired by Japanese furigana — a reading aid that overlays pronunciation hints above kanji characters

---

Built for Indonesian language learners, by Rayhan Rizqi. If this helps you, consider giving it a ⭐
