# Configuration du formulaire de contact avec EmailJS

Le formulaire de contact est maintenant configuré pour envoyer les informations par email en utilisant EmailJS, un service gratuit qui permet d'envoyer des emails depuis des sites statiques.

## Étapes de configuration

### 1. Créer un compte EmailJS

1. Allez sur [https://www.emailjs.com/](https://www.emailjs.com/)
2. Cliquez sur "Sign Up" et créez un compte gratuit
3. Confirmez votre adresse email

### 2. Connecter votre service email

1. Dans le dashboard EmailJS, allez dans **Email Services**
2. Cliquez sur **Add New Service**
3. Choisissez votre fournisseur d'email (Gmail, Outlook, etc.)
4. Suivez les instructions pour connecter votre compte email
5. Notez le **Service ID** (par exemple: `service_abc123`)

### 3. Créer un template d'email

1. Allez dans **Email Templates**
2. Cliquez sur **Create New Template**
3. Configurez le template avec le contenu suivant :

**Subject:** Nouveau message de contact - {{nom}} {{prenom}}

**Body:**
```
Nouveau message reçu depuis le formulaire de contact :

Nom : {{nom}}
Prénom : {{prenom}}
Email : {{email}}
Téléphone : {{telephone}}
Date : {{date}}
Consentement : {{consent}}

Message :
{{message}}

---
Ce message a été envoyé depuis le site Uni.e.s pour Draguignan
```

4. Dans la section **To Email**, entrez l'adresse email où vous souhaitez recevoir les messages (par exemple: `uni.e.spourdraguignan@mailo.com`)
5. Sauvegardez le template et notez le **Template ID** (par exemple: `template_xyz789`)

### 4. Obtenir votre Public Key

1. Allez dans **Account** > **General**
2. Trouvez votre **Public Key** (par exemple: `abc123xyz789`)

### 5. Mettre à jour le code HTML

Dans le fichier `index.html`, remplacez les placeholders suivants :

**Ligne ~405-407 :**
```javascript
emailjs.init('YOUR_PUBLIC_KEY');
```
Remplacez `YOUR_PUBLIC_KEY` par votre Public Key

**Ligne ~433 :**
```javascript
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams)
```
Remplacez :
- `YOUR_SERVICE_ID` par votre Service ID
- `YOUR_TEMPLATE_ID` par votre Template ID

### Exemple de configuration finale :

```javascript
emailjs.init('abc123xyz789');

// ...

emailjs.send('service_abc123', 'template_xyz789', templateParams)
```

## Test du formulaire

1. Ouvrez votre site web
2. Remplissez le formulaire de contact
3. Cochez la case de consentement
4. Cliquez sur "Envoyer"
5. Vous devriez recevoir un email avec les informations du formulaire

## Limites du plan gratuit

Le plan gratuit d'EmailJS permet :
- 200 emails par mois
- 2 email services
- 3 email templates

Pour un usage plus intensif, consultez les plans payants sur [https://www.emailjs.com/pricing/](https://www.emailjs.com/pricing/)

## Alternative : Formspree

Si vous préférez une alternative, vous pouvez utiliser Formspree :

1. Créez un compte sur [https://formspree.io/](https://formspree.io/)
2. Créez un nouveau formulaire
3. Remplacez la balise `<form>` par :
```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST" class="space-y-6">
```

## Support

Pour toute question sur EmailJS, consultez leur documentation : [https://www.emailjs.com/docs/](https://www.emailjs.com/docs/)
