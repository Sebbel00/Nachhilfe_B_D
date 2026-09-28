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
  }
}
```

Hinweis: Diese Regeln erlauben jedem, der die Projektdaten kennt, Zugriff auf die Sammlung `bd_trainer`. Deshalb als Schülernamen am besten ein Kürzel oder nur den Vornamen verwenden.

## 2. GitHub Pages
1. Neues Repository anlegen, `index.html` und `woerter.json` hochladen.
2. Settings → Pages → Source: „Deploy from a branch“, Branch `main`, Ordner `/ (root)`.
3. Eigene Subdomain: unter Settings → Pages → „Custom domain“ eintragen (GitHub legt dabei eine `CNAME`-Datei an). Beim Domain-Anbieter einen CNAME-Eintrag auf `<benutzername>.github.io` setzen. Danach „Enforce HTTPS“ aktivieren.

## 3. Bedienung
- **Lehrerbereich:** oben rechts auf 🧑‍🏫 tippen, PIN eingeben. 
- **Stufen:** Die nächste Stufe schaltet sich automatisch frei, wenn 17 der letzten 20 Wörter der aktuellen Stufe richtig sind (änderbar über `FREI_FENSTER` und `FREI_ZIEL` in `index.html`). Im Lehrerbereich unter „Einstellungen“ lässt sich das abschalten und von Hand freischalten.
- **Wortliste erweitern:** Lehrerbereich → Wortliste → Wort eingeben, b/d-Buchstaben antippen → „Wort hinzufügen“ → „woerter.json herunterladen“. Im Repository: „Add file“ → „Upload files“ → Datei hochladen → „Commit changes“. Nach ca. 1–2 Minuten ist die neue Liste online.
- Bearbeitungen an der Wortliste bleiben auf dem Gerät gespeichert, bis sie hochgeladen oder verworfen werden.
- Neue Wörter starten ohne Lernstand. Der Lernstand hängt am Wort, nicht an der Liste.
