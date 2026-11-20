# Vokabeln

Personal German vocabulary flashcards with spaced repetition (Anki-style SM-2), as a static offline PWA. UI in Spanish. All data stays in the browser's localStorage; there are no external scripts or services.

## Run locally

```
cd vokabeln-app
python3 -m http.server 8090
```

Open http://localhost:8090. The service worker only registers on http(s), so opening the file directly also works (without offline caching). After changing any cached file, bump `CACHE` in `sw.js`.

## Add to iPhone home screen

Serve the folder over https (any static host), open it in Safari, tap Share, then "Add to Home Screen".

## Import format

Paste text or choose a `.txt` / `.csv` / `.tsv` file from the Añadir/Exportar and Copia buttons. The separator (tab, semicolon or comma) is detected automatically. Columns:

```
word;meaning;example;register;tags
der Hund, -e;perro;Der Hund bellt.;;animales
die Frau (pl. Frauen);mujer
```

- A leading der/die/das is split off as the article. Plurals like `, -e`, `, ¨-er` or `(pl. Frauen)` go into the plural field.
- Register: `ugs.`, `sachlich` or `gehoben` (optional). Tags are separated by spaces or commas.
- Lines starting with `#` are skipped, HTML tags are stripped, so Anki's "Notes in Plain Text" export works.
- Duplicates (same article + word) are skipped.

Each note creates two cards (DE→ES and ES→DE). "Pegar lista" turns a pasted list (one entry per line, e.g. from iPhone Live Text) into cards, with a preview and an ES/EN meaning toggle per row. Images are kept in IndexedDB.

Export creates a JSON backup of cards and progress; the same file can be restored from Copia.
