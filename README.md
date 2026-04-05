# Mon École 🎀 — Guide de déploiement

## Structure des fichiers

```
ecole-app/
├── index.html        ← Page principale (menu + navigation)
├── app-mots.html     ← Module dictée
├── admin.html        ← Interface d'administration
├── data.json         ← Base de données des mots (à modifier chaque semaine)
├── netlify.toml      ← Configuration Netlify
└── README.md         ← Ce fichier
```

## Déploiement sur Netlify

### 1. Première installation

1. Crée un compte sur [netlify.com](https://netlify.com) (gratuit)
2. Va dans **"Add new site" → "Deploy manually"**
3. Glisse le dossier `ecole-app/` entier dans la zone de dépôt
4. Netlify te donne une URL (ex: `mon-ecole-xyz.netlify.app`)
5. Tu peux personnaliser l'URL dans Site settings → Domain management

### 2. Mettre à jour les mots de la semaine

**Option A — Via l'interface admin (recommandé) :**
1. Va sur `ton-site.netlify.app/admin.html`
2. Clique sur "Mots de la semaine"
3. Efface les anciens mots, ajoute les nouveaux
4. Clique "Enregistrer" → "Export JSON" → "Télécharger data.json"
5. Redéploie sur Netlify : **Deploys → Drag & drop** le dossier mis à jour

**Option B — Modifier data.json directement :**
Ouvre `data.json` avec un éditeur de texte et modifie le tableau `"motsSemaine"`.

### 3. Structure de data.json

```json
{
  "motsSemaine": ["maison", "jardin", "école"],
  "motsEcole": ["maison", "jardin", "école", "cahier", ...],
  "motsOutils": ["accent", "acheter", "aimer", ...]
}
```

- **motsSemaine** : Les mots de la semaine en cours (remplacer chaque lundi)
- **motsEcole** : Tous les mots vus depuis le début de l'année (ajouter chaque semaine)
- **motsOutils** : La liste CP/CE1 complète (ne change pas souvent)

> ℹ️ La liste "Mots outils" dans l'appli = motsOutils + motsEcole + motsSemaine combinés.

## Fonctionnalités

### Module Mots (dictée)
- 🗓️ **Mots de la semaine** : uniquement les mots récents
- 🏫 **Mots école** : tous les mots vus en classe
- 🛠️ **Mots outils** : grande liste + mots école
- Séries : sans limite / 10 mots / 20 mots
- Vocalisation avec l'API Web Speech (voix française)
- Bouton "Réécouter" à tout moment
- Correction détaillée : caractères corrects en vert, erreurs en rouge
- Bilan de fin de série avec liste des erreurs
- Confettis quand tout est réussi 🎉

### Ajout de modules futurs
Pour ajouter un nouveau module (ex: tables de multiplication) :
1. Crée `app-tables.html`
2. Dans `index.html`, ajoute un bouton dans la `.nav-list`
3. Ajoute `data-page="tables"` et un appel `showPage('tables', this)`
4. Ajoute un `<div class="page" id="page-tables">` avec l'iframe correspondant

## Support navigateurs

- ✅ Chrome / Chromium (meilleur support voix française)
- ✅ Safari (iPad, iPhone, Mac)
- ✅ Firefox
- ⚠️ La voix peut varier selon le système (dépend des voix installées sur l'appareil)
