# b oder d? – Übungsseite

## Dateien
- `index.html` – Übungen, Lehrerbereich, Firebase-Anbindung
- `woerter.json` – Wortliste (wird im Lehrerbereich bearbeitet und hier ersetzt)

## 1. Firebase einrichten
1. In der Firebase-Konsole ein Projekt anlegen (oder ein vorhandenes nutzen).
2. **Firestore Database** erstellen.
3. Projekteinstellungen → „Deine Apps“ → Web-App hinzufügen → die Werte aus `firebaseConfig` oben in `index.html` bei `FIREBASE_CONFIG` eintragen.
4. `LEHRER_PIN` in `index.html` ändern.
5. Firestore → Regeln:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /bd_trainer/{schueler} {
      allow read, write: if true;
    }
    match /bd_woerter/{dokument} {
      allow read, write: if true;
    }
  }
}
```

Hinweis: Diese Regeln erlauben jedem, der die Projektdaten kennt, Zugriff auf die Sammlungen `bd_trainer` und `bd_woerter`. Deshalb als Schülernamen am besten ein Kürzel oder nur den Vornamen verwenden.

## 2. GitHub Pages
1. Neues Repository anlegen, `index.html` und `woerter.json` hochladen.
2. Settings → Pages → Source: „Deploy from a branch“, Branch `main`, Ordner `/ (root)`.
3. Eigene Subdomain: unter Settings → Pages → „Custom domain“ eintragen (GitHub legt dabei eine `CNAME`-Datei an). Beim Domain-Anbieter einen CNAME-Eintrag auf `<benutzername>.github.io` setzen. Danach „Enforce HTTPS“ aktivieren.

## 3. Bedienung
- **Lehrerbereich:** oben rechts auf 🧑‍🏫 tippen, PIN eingeben. 
- **Stufen:** Die nächste Stufe schaltet sich automatisch frei, wenn 17 der letzten 20 Wörter der aktuellen Stufe richtig sind (änderbar über `FREI_FENSTER` und `FREI_ZIEL` in `index.html`). Im Lehrerbereich unter „Einstellungen“ lässt sich das abschalten und von Hand freischalten.
- **Wortliste erweitern:** Lehrerbereich → Wortliste → Wort eingeben, b/d-Buchstaben antippen → „Wort hinzufügen“. Die Liste wird sofort in Firebase (`bd_woerter/liste`) gespeichert und gilt auf allen Geräten.
- Die `woerter.json` im Repository dient nur noch als Startliste, solange in Firebase noch keine Liste existiert. „Als Datei herunterladen“ erstellt eine Sicherung, „Datei importieren“ spielt eine Sicherung wieder ein.
- Ist Firebase nicht erreichbar, bleiben Änderungen auf dem Gerät zwischengespeichert, bis „In Firebase speichern“ klappt.
- Neue Wörter starten ohne Lernstand. Der Lernstand hängt am Wort, nicht an der Liste.
