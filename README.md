# Site SADE France

Site institutionnel de **SADE — Service d'Accompagnement des Démarches Étrangères**.
Site statique HTML/CSS/JS, sans framework, prêt à être hébergé n'importe où (OVH, o2switch, Netlify, GitHub Pages, etc.).

---

## 📁 Structure du projet

```
sade-france-site/
├── index.html              ← Page d'accueil
├── cabinet.html            ← Présentation du cabinet
├── services.html           ← Détail des 4 services
├── contact.html            ← Formulaire de contact
├── merci.html              ← Page de confirmation après envoi du formulaire
├── mentions-legales.html   ← Mentions légales (LCEN)
├── confidentialite.html    ← Politique de confidentialité (RGPD)
├── styles.css              ← Feuille de style commune à toutes les pages
├── README.md               ← Ce document
└── assets/
    ├── logo-cropped.png        ← Logo principal (texte noir) — pour fond clair
    ├── logo-light-text.png     ← Logo (texte blanc) — pour fond bleu/sombre
    ├── logo.png                ← Logo original avec fond noir (sauvegarde)
    ├── favicon.png             ← Favicon 256×256 (juste l'hexagone "S")
    ├── favicon-32.png          ← Favicon 32×32
    ├── favicon-16.png          ← Favicon 16×16
    ├── apple-touch-icon.png    ← Icône iOS 180×180
    └── og-image.png            ← Image affichée lors du partage du site (1200×630)
```

---

## 🚀 Mise en ligne

**Le site est entièrement statique.** Pour le mettre en ligne :

1. **Téléverser tous les fichiers** (HTML, CSS, dossier `assets/`) dans la racine de votre hébergement web via FTP/SFTP.
2. C'est tout — pas de base de données, pas de configuration.

Hébergeurs recommandés :
- **OVH / o2switch / Hostinger** : hébergement classique mutualisé (~3-5 €/mois)
- **Netlify / Vercel / Cloudflare Pages** : gratuit pour ce type de site, très rapide
- **GitHub Pages** : gratuit si le site est dans un dépôt GitHub

---

## 🎨 Charte graphique

Tout est centralisé dans `styles.css` via des variables CSS au début du fichier (`:root`).
Pour changer une couleur ou une typo dans tout le site, modifiez juste la variable correspondante.

| Variable CSS  | Valeur     | Usage                             |
| ------------- | ---------- | --------------------------------- |
| `--c-blue`    | `#2F1BF9`  | Bleu électrique (couleur primaire) |
| `--c-indigo`  | `#1E0BC5`  | Indigo profond (effets décoratifs) |
| `--c-black`   | `#030303`  | Texte principal                   |
| `--c-white`   | `#FFFFFF`  | Fond clair                        |
| `--c-gray`    | `#E8E8E6`  | Bordures et lignes                |
| `--c-gray-2`  | `#F5F5F3`  | Fonds gris clair                  |

**Police :** Codec Pro (charte officielle).
Comme c'est une police commerciale Zetafonts, j'ai mis **Space Grotesk** (Google Fonts, gratuit) en remplacement temporaire — elle est très proche visuellement.

Pour utiliser Codec Pro pour de vrai :
1. Acheter la licence sur https://www.zetafonts.com/codec
2. Récupérer les fichiers `.woff2`
3. Les ajouter dans `assets/fonts/` et déclarer un `@font-face` en haut de `styles.css`
4. Modifier la variable `--font` pour pointer vers `'Codec Pro'` en premier

---

## 📝 Modifier le contenu

### Modifier les coordonnées (téléphone, email, adresse)

Les coordonnées apparaissent sur **plusieurs pages** : `contact.html`, `mentions-legales.html`, `confidentialite.html` et `merci.html`.

**Remplacer le téléphone** : faire une recherche globale sur `+33 6 49 63 84 03` et `+33649638403` (version sans espaces utilisée dans les liens `tel:`).

**Remplacer l'email** : recherche globale sur `contact@sade78.fr`.

**Remplacer l'adresse** : recherche globale sur `5 rue Charles Denet` et `27000 Évreux`.

### Modifier la page d'accueil

Ouvrir `index.html`. Les commentaires `<!-- 🔧 ... -->` indiquent les zones à modifier :

- **Titre principal (h1)** : ligne `<h1>Votre partenaire pour vos démarches...</h1>`
- **Chiffres clés** : chercher `<div class="hero-stats">` (3 stats)
- **Cartes services** : chercher `<div class="services-grid">` (4 cartes)

### Modifier les services

Dans `services.html`, chaque service est dans un bloc `<div class="svc-content" data-content="XXX">` où XXX vaut :
- `titre` → Titre de séjour
- `naturalisation`
- `regroupement`
- `asile`

Pour ajouter un 5ème service :
1. Dans `<div class="svc-tabs">`, dupliquer un `<button class="svc-tab">` avec un nouveau `data-tab="xxx"`
2. Dupliquer un `<div class="svc-content">` avec le même `data-content="xxx"`
3. Le JS en bas de page gère automatiquement la bascule entre onglets

### Modifier les valeurs / chiffres du cabinet

Dans `cabinet.html` : commentaires `<!-- 🔧 ... -->` au-dessus de chaque section.

### Modifier les mentions légales / la confidentialité

Ouvrir `mentions-legales.html` ou `confidentialite.html`. Chaque section est entourée de `<div class="legal-section">`. Les blocs jaunes "À compléter" sont dans `<div class="legal-note">`.

**⚠️ Deux choses à compléter avant la mise en ligne** :
1. **Hébergeur** dans `mentions-legales.html` → c'est une obligation légale (LCEN art. 6)
2. **Médiateur de la consommation** dans `mentions-legales.html` → obligatoire pour les pros traitant avec des particuliers

---

## 📧 Activer l'envoi du formulaire de contact

Pour le moment, le formulaire **affiche uniquement la page de confirmation** sans envoyer d'email. Pour activer l'envoi réel, vous avez 3 options :

### Option 1 : Formspree (le plus simple, recommandé)

1. Créer un compte gratuit sur https://formspree.io
2. Récupérer votre identifiant de formulaire (ex : `xqkrabcd`)
3. Dans `contact.html`, modifier la balise `<form>` :
   ```html
   <form id="contactForm" action="https://formspree.io/f/xqkrabcd" method="POST">
   ```
4. Ajouter un champ caché pour rediriger vers `merci.html` :
   ```html
   <input type="hidden" name="_next" value="https://sade78.fr/merci.html">
   ```
5. Supprimer le script JS de gestion du submit en bas de page (Formspree gère tout).

Tarif : gratuit jusqu'à 50 messages/mois, puis 10 $/mois pour 1000 messages.

### Option 2 : Script PHP (si votre hébergeur supporte PHP)

Créer un fichier `mail.php` dans la racine, et modifier la balise `<form>` :
```html
<form id="contactForm" action="mail.php" method="POST">
```

### Option 3 : Fonction serverless (Netlify Forms / Vercel Functions)

Si vous hébergez sur Netlify, ajouter `data-netlify="true"` au `<form>` et tout est géré automatiquement.

---

## 🎯 SEO & partage

Chaque page a ses balises **Open Graph** correctement définies (image `og-image.png`, titre, description). Quand quelqu'un partage le site sur WhatsApp, LinkedIn, Facebook, Twitter, Discord, Slack… une jolie carte avec le logo et le tagline apparaît automatiquement.

**Pour modifier l'image de partage** : remplacer `assets/og-image.png` par un PNG **1200×630 px**.

**Pour modifier le titre/description de partage** : voir les `<meta property="og:title">` et `og:description` dans le `<head>` de chaque page.

---

## 📱 Comportement responsive

Le site est conçu en **« no-scroll » sur desktop** (chaque page tient sur un écran 100vh) et en **scroll naturel sur mobile** (≤ 860 px) pour ne pas tasser le contenu sur petit écran.

Le breakpoint est défini à **860 px** dans `styles.css` :
- Au-dessus : layout en 2 colonnes côte à côte, hauteur fixe `100dvh`
- En dessous : empilement vertical, scroll natif autorisé, header sticky avec blur

Sur la page Services, la sidebar avec onglets devient un **accordéon** sur mobile.

---

## 🔧 Modifier le breakpoint mobile

Si vous voulez changer la limite à laquelle le site bascule en mode mobile (par défaut 860 px), faites une recherche-remplacement sur `860px` dans `styles.css` et dans chaque page HTML (chaque page a aussi des règles spécifiques en `@media (max-width:860px)`).

---

## 🆘 Problèmes courants

### Le logo se déforme
Vérifier que `object-fit: contain` est bien présent dans `.logo-img` du CSS. Le logo a un ratio de 2.6:1 et ne doit jamais être étiré.

### Les couleurs ne se mettent pas à jour
Vider le cache du navigateur (Ctrl+F5). Les variables CSS sont rechargées au refresh forcé.

### Le formulaire envoie mais rien ne se passe
Vous n'avez pas encore branché un service d'envoi (voir la section "Activer l'envoi du formulaire" plus haut). Pour le moment, seule la page `merci.html` s'affiche, mais aucun email n'est envoyé.

### L'image Open Graph n'apparaît pas dans les partages
Les réseaux sociaux mettent en cache l'image. Pour forcer le rafraîchissement :
- Facebook : https://developers.facebook.com/tools/debug/
- LinkedIn : https://www.linkedin.com/post-inspector/
- Twitter : https://cards-dev.twitter.com/validator

---

## 📋 Checklist avant la mise en ligne

- [ ] Compléter le **nom de l'hébergeur** dans `mentions-legales.html`
- [ ] Souscrire et indiquer un **médiateur de la consommation**
- [ ] Brancher l'envoi réel du **formulaire de contact** (Formspree ou autre)
- [ ] Vérifier que l'**URL canonique** dans les balises Open Graph correspond à votre vrai domaine (par défaut : `https://sade78.fr/`)
- [ ] Acheter la licence **Codec Pro** (optionnel — Space Grotesk fonctionne très bien en remplacement)
- [ ] Tester le site sur **mobile réel** (iPhone et Android)
- [ ] Vérifier les **mentions légales** avec votre comptable ou un juriste
- [ ] Activer **HTTPS** sur votre hébergement (Let's Encrypt est gratuit)

---

## 📞 Contact technique

Pour toute question technique sur le site, vous pouvez consulter :
- La documentation MDN : https://developer.mozilla.org/fr/
- Documentation Formspree : https://help.formspree.io/

---

**Version :** 1.0
**Dernière mise à jour :** Mai 2026
