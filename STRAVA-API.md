# Configuration Strava API — Objectif Run

## Champs sur https://www.strava.com/settings/api

| Champ | Valeur |
|-------|--------|
| **Application Name** | Objectif Run |
| **Category** | Training |
| **Website** | `https://monobjectifrun.github.io/` |
| **Authorization Callback Domain** | Voir ci-dessous |

---

## Website (site web)

Utilise l’URL GitHub Pages une fois déployé :

```
https://monobjectifrun.github.io/
```

Page confidentialité (utile App Store + Strava) :

```
https://monobjectifrun.github.io/privacy.html
```

---

## Authorization Callback Domain

### Développement avec Expo Go (téléphone)

Ce n’est **pas** le domaine GitHub.

1. Lance l’app → écran « Connecte Strava »
2. Note l’**IP affichée** (ex. `192.168.1.151`)
3. Mets **uniquement cette IP** dans Strava (sans `http`, sans port)

### Production (app compilée)

Option A — schéma custom (recommandé plus tard) :

- Callback domain : `localhost` (souvent accepté par Strava pour mobile)
- Redirect URI dans l’app : `objectifrun://redirect` (à aligner avec `app.json` → `scheme`)

Option B — redirect HTTPS via GitHub Pages (avancé) :

- Callback domain : `monobjectifrun.github.io`
- Redirect URI : `https://monobjectifrun.github.io/auth/callback`

Pour l’instant, garde l’**IP locale** pour Expo Go.

---

## Variables `.env` (app mobile)

```env
EXPO_PUBLIC_STRAVA_CLIENT_ID=...
EXPO_PUBLIC_STRAVA_CLIENT_SECRET=...
```
