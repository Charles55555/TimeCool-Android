# TimeCool — Application Android (test)

> *"Le temps est la seule ressource qu'on ne peut jamais fabriquer."*

Ce dossier contient **deux livrables** pour tester TimeCool sur smartphone :

1. **PWA** (dans `pwa/`) — installable en 30 secondes sur Android via Chrome.
2. **Projet Android Studio complet** (dossiers `app/`, `build.gradle`, etc.) — pour générer une vraie APK `.apk` à installer.

---

## 🟢 Option 1 — PWA (la plus rapide, testable maintenant)

La PWA est une vraie application Android (icône sur l'écran d'accueil, plein écran, hors-ligne) installée depuis Chrome.

**Étapes :**
1. Hébergez le dossier `pwa/` sur **n'importe quel serveur HTTPS** (Netlify, Vercel, GitHub Pages, OVH…). Trois clics avec Netlify Drop : https://app.netlify.com/drop → glissez le dossier `pwa/`.
2. Sur votre smartphone Android, ouvrez l'URL dans **Chrome**.
3. Menu Chrome (⋮) → **« Installer l'application »** ou **« Ajouter à l'écran d'accueil »**.
4. L'icône TimeCool apparaît sur l'écran d'accueil. Tap → l'app s'ouvre en plein écran, comme une vraie app.

**Note** : la PWA fonctionne aussi **hors-ligne** grâce au service worker (`sw.js`).

---

## 🔵 Option 2 — APK via GitHub Actions (recommandé, zéro install locale)

Vous obtenez un vrai fichier `.apk` signé, sans rien installer sur votre PC.

**Étapes :**
1. Créez un repo GitHub (privé ou public).
2. Uploadez tout le contenu de ce dossier (`TimeCool-Android/*`).
3. Allez dans l'onglet **Actions** du repo : le workflow `Build TimeCool APK` se lance automatiquement (~3-5 min).
4. Une fois terminé, ouvrez le run → section **Artifacts** → téléchargez `TimeCool-debug-apk.zip`.
5. Décompressez → vous avez `app-debug.apk`.
6. Transférez sur votre Android (mail, USB, Drive) et ouvrez le fichier.
7. Acceptez « Sources inconnues » dans les paramètres → Installer.

Le workflow est déjà prêt dans `.github/workflows/build-apk.yml`. Vous n'avez rien à configurer.

---

## 🟣 Option 3 — APK via Android Studio (en local)

Si vous avez (ou souhaitez installer) **Android Studio** :

1. Téléchargez Android Studio : https://developer.android.com/studio
2. **File → Open** → sélectionnez ce dossier `TimeCool-Android/`.
3. Attendez la synchro Gradle (~2 min la première fois).
4. **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
5. Cliquez sur le lien « locate » dans la notif → vous trouvez `app-debug.apk` dans `app/build/outputs/apk/debug/`.
6. Branchez votre téléphone en USB (mode débug activé) et **Run → Run 'app'**, ou copiez l'APK manuellement.

---

## 📁 Structure du projet

```
TimeCool-Android/
├── README.md                    ← ce fichier
├── build.gradle                 ← config Gradle racine
├── settings.gradle
├── gradle.properties
├── .gitignore
├── .github/
│   └── workflows/
│       └── build-apk.yml        ← build automatique cloud
├── app/
│   ├── build.gradle             ← config Gradle module
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/timecool/app/
│       │   └── MainActivity.java   ← Activity unique : WebView plein écran
│       ├── res/
│       │   ├── mipmap-*/           ← icônes launcher (5 densités)
│       │   ├── values/             ← strings, colors, styles
│       │   └── xml/
│       └── assets/
│           └── index.html          ← démo TimeCool v4.1 embarquée
└── pwa/                         ← version PWA
    ├── index.html               ← démo + manifest + SW
    ├── manifest.webmanifest
    ├── sw.js
    └── icons/                   ← jeu d'icônes PNG
```

---

## ⚙️ Caractéristiques techniques

| | Valeur |
|---|---|
| **Nom de l'app** | TimeCool |
| **Package** | `com.timecool.app` |
| **Version** | 1.0.0-test |
| **Min Android** | 7.0 (API 24) — couvre 98%+ des téléphones |
| **Cible Android** | 14 (API 34) |
| **Permissions** | INTERNET uniquement |
| **Architecture** | WebView native (zéro framework lourd) |
| **Taille APK estimée** | ~250 Ko |

---

## 🎯 Ce que contient la démo (HTML embarquée v4.1)

- Onboarding Assistant IA ludique
- 3 cas d'usage : RDV particulier, gestion pro retards/annulations, réunion multi-personnes
- Partage sélectif d'informations (coffre-fort intelligent)
- Système de notation privée bilatérale
- Identité visuelle Google (couleurs `#1a73e8` `#ea4335` `#fbbc04` `#34a853`)
- Chiffrement E2E affiché en permanence

---

## 🧪 Pour tester rapidement

**Le plus rapide en absolu** : option 1 (PWA via Netlify Drop) — vous avez l'app sur votre téléphone en moins de 2 minutes.

**Le plus "vraie app"** : option 2 (GitHub Actions) — vrai .apk signé, prêt pour distribution beta.

---

## ⚠️ Note importante

Cette version est un **prototype de démonstration** (HTML statique dans une WebView).
La version production nécessitera :
- Backend (auth, agendas, sync E2E)
- IA conversationnelle réelle (LLM + matching d'agendas)
- Notifications push (FCM)
- Build release signé avec keystore officielle
- Publication Play Store

Le brief v2 (`TimeCool_Brief_v2.md`) reste la référence de la vision finale.
