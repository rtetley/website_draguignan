# Configuration du déploiement automatique vers OVH

Ce projet utilise GitHub Actions pour déployer automatiquement le site web vers OVH Cloud via FTP à chaque push sur la branche `main` ou `master`.

## Étape 1 : Obtenir vos informations FTP OVH

1. Connectez-vous à votre espace client OVH
2. Allez dans **Web Cloud** > **Hébergements**
3. Sélectionnez votre hébergement
4. Dans l'onglet **FTP-SSH**, notez les informations suivantes :
   - **Serveur FTP** (exemple : `ftp.votredomaine.com` ou `ftp.cluster0XX.hosting.ovh.net`)
   - **Login FTP** (exemple : `votrenom` ou `votredomaine.com`)
   - **Mot de passe FTP** (si vous ne l'avez pas, vous pouvez le réinitialiser)

## Étape 2 : Configurer les secrets GitHub

1. Allez sur votre dépôt GitHub
2. Cliquez sur **Settings** (Paramètres)
3. Dans le menu latéral, cliquez sur **Secrets and variables** > **Actions**
4. Cliquez sur **New repository secret** et ajoutez les secrets suivants :

### Secret 1 : FTP_SERVER
- **Name:** `FTP_SERVER`
- **Value:** L'adresse de votre serveur FTP (exemple : `ftp.cluster0XX.hosting.ovh.net`)

### Secret 2 : FTP_USERNAME
- **Name:** `FTP_USERNAME`
- **Value:** Votre identifiant FTP (exemple : `votrenom`)

### Secret 3 : FTP_PASSWORD
- **Name:** `FTP_PASSWORD`
- **Value:** Votre mot de passe FTP

⚠️ **Important** : Ne partagez jamais ces informations et ne les commitez jamais dans le code !

## Étape 3 : Ajuster le répertoire de destination (si nécessaire)

Par défaut, le workflow déploie dans le répertoire racine (`./`). Si vous devez déployer dans un sous-répertoire spécifique sur OVH (par exemple `/www/` ou `/public_html/`), modifiez la ligne `server-dir` dans `.github/workflows/deploy.yml` :

```yaml
server-dir: ./www/  # ou ./public_html/ selon votre configuration OVH
```

## Étape 4 : Tester le déploiement

### Déploiement automatique
Une fois les secrets configurés, le site sera automatiquement déployé à chaque fois que vous poussez des changements sur la branche `main` ou `master` :

```bash
git add .
git commit -m "Update website"
git push origin main
```

### Déploiement manuel
Vous pouvez aussi déclencher un déploiement manuellement :

1. Allez dans l'onglet **Actions** de votre dépôt GitHub
2. Sélectionnez le workflow **Deploy to OVH via FTP**
3. Cliquez sur **Run workflow**
4. Choisissez la branche et cliquez sur **Run workflow**

## Étape 5 : Vérifier le déploiement

1. Une fois le workflow terminé (vous verrez une coche verte ✓), votre site est en ligne
2. Visitez votre site web sur votre domaine OVH
3. En cas d'erreur, consultez les logs dans l'onglet **Actions** de GitHub

## Structure du workflow

Le workflow effectue les actions suivantes :

1. **Checkout** : Récupère le code source
2. **Setup Node.js** : Installe Node.js version 20
3. **Install dependencies** : Installe les dépendances npm
4. **Build** : Compile le projet avec Vite (crée le dossier `build/`)
5. **Deploy** : Envoie les fichiers du dossier `build/` vers OVH via FTP

## Configuration avancée

### Déployer uniquement des fichiers spécifiques

Pour exclure certains fichiers du déploiement, modifiez la section `exclude` dans `.github/workflows/deploy.yml` :

```yaml
exclude: |
  **/.git*
  **/.git*/**
  **/node_modules/**
  **/.vscode/**
  **/.DS_Store
  **/README.md
  **/*.log
```

### Nettoyer le serveur avant déploiement

Si vous voulez supprimer les anciens fichiers avant chaque déploiement (⚠️ attention, cela supprime tout le contenu du répertoire cible) :

```yaml
dangerous-clean-slate: true
```

### Déployer vers plusieurs environnements

Pour avoir des environnements de staging et production, créez plusieurs workflows avec des branches différentes :

- `deploy-staging.yml` : déclenché sur la branche `develop`
- `deploy-production.yml` : déclenché sur la branche `main`

## Dépannage

### Erreur "Authentication failed"
- Vérifiez que vos identifiants FTP sont corrects
- Assurez-vous que les secrets GitHub sont bien configurés
- Essayez de vous connecter manuellement via un client FTP (FileZilla) pour valider les identifiants

### Erreur "Connection timeout"
- Vérifiez que le serveur FTP est accessible
- Certains hébergeurs OVH nécessitent une IP autorisée (vérifiez dans votre espace client OVH)

### Les fichiers ne s'affichent pas
- Vérifiez que le `server-dir` pointe vers le bon répertoire (souvent `/www/` ou `/public_html/` chez OVH)
- Consultez les logs du workflow pour voir où les fichiers ont été déployés

### Le build échoue
- Vérifiez que toutes les dépendances sont dans `package.json`
- Testez le build en local : `npm run build`

## Ressources

- [Documentation OVH - FTP](https://docs.ovh.com/fr/hosting/connexion-espace-stockage-ftp-hebergement-web/)
- [GitHub Actions - Documentation](https://docs.github.com/en/actions)
- [FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action)

## Support

Si vous rencontrez des problèmes, consultez les logs du workflow dans l'onglet **Actions** de GitHub pour identifier l'erreur exacte.
