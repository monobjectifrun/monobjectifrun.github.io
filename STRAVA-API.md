# Configuration Strava API — Mon Objectif Run

## Champs sur https://www.strava.com/settings/api

| Champ | Valeur |
|-------|--------|
| **Application Name** | Mon Objectif Run |
| **Category** | Training |
| **Website** | `https://monobjectifrun.github.io/` |
| **Authorization Callback Domain** | Voir ci-dessous |

---

## Authorization Callback Domain

L’app affiche la valeur exacte à copier sur l’écran **Connecte Strava**.

| Mode | Callback Domain | redirect_uri (automatique) |
|------|-----------------|----------------------------|
| **TestFlight / App Store / build installé** | **`monobjectifrun.github.io`** | `https://monobjectifrun.github.io/strava.html` |
| **Expo Go** (dev) | IP affichée (ex. `192.168.1.42`) | `exp://…/--/redirect` |

Pas de `http://`, pas de port, pas de chemin — **uniquement le domaine** (ou l’IP).

---

## Pourquoi GitHub Pages ?

Strava **n’accepte pas** les schémas custom (`monobjectifrun://`) comme redirect_uri. Il exige un vrai domaine.

Solution standard mobile :

1. Strava redirige vers `https://monobjectifrun.github.io/strava.html?code=...`
2. La page `strava.html` (dans `docs/`) **rebondit automatiquement** vers `monobjectifrun://strava?code=...`
3. iOS / Android rouvre Mon Objectif Run avec le code → connexion terminée.

Fichiers concernés :

- `docs/strava.html` — page de rebond (déployée sur GitHub Pages)
- `src/data/strava/config.ts` — URLs OAuth
- `src/data/strava/auth.ts` — flux d’authentification

---

## Prérequis : GitHub Pages déployé

Le repo `monobjectifrun.github.io` (ou la branche `gh-pages`) doit servir le dossier `docs/`. Tester dans Safari :

- https://monobjectifrun.github.io/strava.html → doit afficher « Retour vers Mon Objectif Run… »
- https://monobjectifrun.github.io/privacy.html → confidentialité

---

## Variables `.env`

```env
EXPO_PUBLIC_STRAVA_CLIENT_ID=...
EXPO_PUBLIC_STRAVA_CLIENT_SECRET=...
```

Redémarrer Metro après modification (`npx expo start -c`).

---

## Dépannage

| Erreur | Cause | Solution |
|--------|--------|----------|
| `redirect_uri invalid` | Callback Domain ≠ `monobjectifrun.github.io` | Mettre exactement `monobjectifrun.github.io` dans Strava |
| Page blanche après login | `strava.html` pas en ligne (404) ou ancien build | Déployer GitHub Pages + rebuild EAS |
| `code invalid` au token | `.env` incorrect | Vérifier Client ID / Secret |
| Connexion annulée immédiate | Navigation manuelle dans la session d’auth | Relancer « Connecter Strava » |

---

## Changer de mode

- **TestFlight / App Store** : Strava → `monobjectifrun.github.io`
- **Retour Expo Go** : Strava → IP affichée dans l’app (change si l’IP Metro change)
