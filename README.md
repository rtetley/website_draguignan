# Uni.e.s pour Draguignan

Site web officiel pour la campagne des élections municipales de Draguignan.

## 📋 Description

Site web statique présentant le mouvement citoyen "Uni.e.s pour Draguignan", incluant :
- Présentation du mouvement
- Biographie de la tête de liste
- Formulaire de contact
- Liens vers les réseaux sociaux

## 🛠️ Technologies

- **HTML5** - Structure du site
- **Tailwind CSS** - Framework CSS pour le styling
- **Vite** - Build tool et serveur de développement
- **PostCSS** - Traitement CSS avec Autoprefixer

## 📦 Installation

Installez les dépendances avec Yarn :

```bash
yarn install
```

## 🚀 Développement

Pour lancer le serveur de développement :

```bash
yarn dev
```

Le site sera accessible sur `http://localhost:5173`

Le serveur de développement recharge automatiquement la page lors des modifications.

## 🏗️ Build

Pour créer une version optimisée pour la production :

```bash
yarn build
```

Les fichiers de production seront générés dans le dossier `build/`.

## 👀 Prévisualisation

Pour prévisualiser la version de production localement :

```bash
yarn build
yarn serve
```

Le site sera accessible sur `http://localhost:4173`

## 📁 Structure du projet

```
website_draguignan/
├── src/
│   └── input.css           # Fichier CSS source avec Tailwind
├── fonts/
│   ├── Barlow/             # Police Barlow
│   └── Barlow_Condensed/   # Police Barlow Condensed
├── build/                  # Dossier de build (généré)
├── index.html              # Page principale
├── package.json            # Dépendances et scripts
├── vite.config.js          # Configuration Vite
├── tailwind.config.js      # Configuration Tailwind CSS
├── postcss.config.js       # Configuration PostCSS
└── README.md               # Ce fichier
```

## 🎨 Personnalisation

### Polices

Le site utilise les polices Barlow et Barlow Condensed stockées localement dans le dossier `fonts/`.

### Couleurs

Les couleurs principales du thème sont configurées avec Tailwind CSS :
- Violet : `purple-600`
- Bleu : `blue-600`
- Rose : `pink-600`

Pour modifier les couleurs, éditez les classes Tailwind dans `index.html` ou étendez la configuration dans `tailwind.config.js`.

## 📝 Scripts disponibles

- `yarn dev` - Lance le serveur de développement
- `yarn build` - Génère la version de production
- `yarn preview` - Prévisualise la version de production (alias)
- `yarn serve` - Prévisualise la version de production depuis le dossier build

## 🌐 Déploiement

Pour déployer le site, uploadez simplement le contenu du dossier `build/` sur votre serveur web après avoir exécuté `yarn build`.

## 📄 Licence

© 2025 Uni.e.s pour Draguignan - Tous droits réservés
