<p align="center">
  <img src="https://img.shields.io/badge/%E2%99%BF-Guide_d'utilisation-8B5CF6?style=for-the-badge&labelColor=1a1a2e" alt="Guide d'utilisation">
</p>

<h1 align="center">Guide d'utilisation des Skills RGAA</h1>

<p align="center">
  <strong>Deux méthodes, un même objectif : rendre votre site accessible</strong>
</p>

<p align="center">
  <a href="#-méthode-1--audit-sur-le-code-source-claude-code"><img src="https://img.shields.io/badge/Méthode_1-Code_source-10B981?style=flat-square" alt="Code source"></a>
  <a href="#-méthode-2--audit-sur-le-navigateur-claude-in-chrome"><img src="https://img.shields.io/badge/Méthode_2-Navigateur-3B82F6?style=flat-square" alt="Navigateur"></a>
  <a href="#-combiner-les-deux-méthodes"><img src="https://img.shields.io/badge/Workflow_combiné-→-F59E0B?style=flat-square" alt="Workflow combiné"></a>
</p>

<p align="center">
  <sub>← Retour au <a href="README.md">README</a> pour la vue d'ensemble et la liste des 13 thématiques</sub>
</p>

---

<br>

## 🗺️ Quelle méthode choisir ?

| | Méthode 1 — Claude Code | Méthode 2 — Claude in Chrome |
|:---|:---|:---|
| **Quand l'utiliser** | Vous êtes développeur sur le projet | Vous auditez un site tiers ou en production |
| **Accès nécessaire** | Code source (local ou dépôt Git) | Juste une URL dans votre navigateur |
| **Ce qui est analysé** | Fichiers HTML/JSX/Vue/Svelte statiques | Le DOM rendu en temps réel |
| **Avantage clé** | Peut corriger le code directement | Voit exactement ce que l'utilisateur voit |
| **Contenu dynamique** | Analyse le code, pas le rendu | Analyse le rendu après interactions |
| **Idéal pour** | Intégration continue, corrections en dev | Recette, audit externe, vérification |

Les deux méthodes utilisent les mêmes skills et appliquent les mêmes 106 critères. Seul le mode d'accès aux données change.

<br>

---

<br>

## 🖥️ Méthode 1 — Audit sur le code source (Claude Code)

### Pour qui ?

Vous êtes développeur, vous avez accès au code du projet, et vous voulez vérifier et corriger l'accessibilité directement dans vos fichiers source.

### Prérequis

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installé (CLI)
- Les fichiers `.skill` installés dans votre configuration Claude Code
- Votre projet cloné localement

### Étape 1 : Installer les skills

Depuis le dossier du dépôt, installez chaque skill :

```bash
# Installer un skill individuel
claude install-skill dist/rgaa-images.skill

# Ou installer tous les skills d'un coup
for skill in dist/*.skill; do
  claude install-skill "$skill"
done
```

### Étape 2 : Naviguer vers votre projet

```bash
cd /chemin/vers/mon-projet
claude
```

### Étape 3 : Lancer un audit

Une fois dans Claude Code, vous pouvez demander des audits à différents niveaux de granularité :

#### Audit d'un fichier spécifique

```
Vérifie l'accessibilité des images dans src/components/Hero.jsx
```

Claude va lire le fichier, identifier les balises `<img>`, `<svg>`, `<canvas>` etc., et vérifier les critères 1.1 à 1.9 du RGAA.

#### Audit d'un composant de formulaire

```
Audite l'accessibilité du formulaire dans src/pages/Contact.vue selon le RGAA
```

Claude va vérifier les étiquettes, le regroupement des champs, les messages d'erreur, les attributs `autocomplete`, etc.

#### Audit global d'une page

```
Analyse tous les fichiers qui composent la page d'accueil 
et fais un audit RGAA complet
```

#### Audit ciblé sur une thématique

```
Vérifie la structure des titres et les landmarks dans tout le dossier src/layouts/
```

#### Scan du projet entier

```
Parcours le dossier src/ et liste toutes les images sans attribut alt
```

### Étape 4 : Corriger directement

L'avantage majeur de Claude Code : il peut **corriger le code pour vous** :

```
Corrige tous les problèmes d'accessibilité que tu as trouvés 
dans src/components/Header.jsx
```

```
Ajoute les attributs aria-label manquants sur tous les liens icônes du projet
```

```
Restructure les titres de src/pages/About.astro pour respecter la hiérarchie RGAA
```

### Exemples concrets par thématique

<details>
<summary><strong>🖼️ Images</strong> — Critères 1.1 à 1.9</summary>

```
Vérifie que toutes les images dans src/ ont un attribut alt pertinent.
Signale celles qui semblent décoratives mais n'ont pas alt="".
```

Claude va scanner les fichiers, trouver les balises images, et distinguer les images informatives des images décoratives en analysant le contexte (icônes dans des boutons, illustrations avec légende, etc.).

</details>

<details>
<summary><strong>🎨 Couleurs</strong> — Critères 3.1 à 3.3</summary>

```
Analyse les fichiers CSS/SCSS du projet et identifie les combinaisons 
de couleur texte/fond qui ne respectent pas les ratios RGAA 
(4.5:1 pour le texte normal, 3:1 pour le texte large).
```

Claude va parser les feuilles de styles, extraire les paires `color`/`background-color`, calculer les ratios et signaler les non-conformités.

</details>

<details>
<summary><strong>📝 Formulaires</strong> — Critères 11.1 à 11.13</summary>

```
Audite tous les formulaires du dossier src/components/forms/ :
- Chaque champ a-t-il une étiquette ?
- Les labels sont-ils associés avec for/id ?
- Les champs obligatoires sont-ils indiqués avec aria-required ?
- Y a-t-il des attributs autocomplete sur les champs personnels ?
```

</details>

<details>
<summary><strong>🏗️ Structure</strong> — Critères 9.1 à 9.4</summary>

```
Affiche la hiérarchie des titres (h1-h6) de src/pages/index.html 
et signale les sauts de niveaux.
Vérifie aussi la présence des landmarks (header, nav, main, footer).
```

</details>

<details>
<summary><strong>🧭 Navigation</strong> — Critères 12.1 à 12.11</summary>

```
Vérifie que le layout principal (src/layouts/Base.astro) contient :
- Un lien d'évitement vers le contenu principal
- Des landmarks labellisés
- Pas de tabindex positif
```

</details>

### Intégration dans le workflow de développement

Vous pouvez intégrer les audits dans votre processus de développement :

```bash
# Avant chaque commit : vérification rapide
claude -p "Vérifie l'accessibilité RGAA des fichiers modifiés dans le dernier commit"

# En revue de code : audit du diff
claude -p "Audite les changements de la PR #42 pour les régressions d'accessibilité"

# En CI : audit complet
claude -p "Lance un audit RGAA complet sur src/ et génère un rapport markdown"
```

<br>

---

<br>

## 🌐 Méthode 2 — Audit sur le navigateur (Claude in Chrome)

### Pour qui ?

Vous auditez un site en production, un site tiers, ou vous voulez vérifier ce que l'utilisateur voit réellement dans son navigateur — contenu dynamique, JavaScript exécuté, CSS appliqué.

### Prérequis

- Google Chrome
- L'extension [Claude in Chrome](https://chromewebstore.google.com/detail/claude/danfoghcmhhmjbkbkclhbjcebfmpgaef) installée
- Les fichiers `.skill` installés dans vos paramètres Claude

### Étape 1 : Installer les skills

1. Ouvrez [claude.ai](https://claude.ai)
2. Allez dans **Paramètres** → **Skills**
3. Cliquez sur **Ajouter un skill**
4. Glissez-déposez les fichiers `.skill` depuis le dossier `dist/`

### Étape 2 : Ouvrir le site à auditer

Naviguez simplement vers le site dans Chrome :

```
https://mon-site.fr/page-a-auditer
```

### Étape 3 : Lancer l'audit

Ouvrez le panneau Claude in Chrome et demandez :

#### Audit complet de la page

```
Fais un audit d'accessibilité RGAA complet de cette page
```

Claude va automatiquement :
1. Exécuter les scripts JavaScript d'extraction de chaque thématique
2. Collecter les éléments du DOM, les styles calculés, les attributs ARIA
3. Appliquer les critères du RGAA
4. Générer un rapport structuré

#### Audit par thématique

```
Audite les images de cette page selon le RGAA
```

```
Vérifie les contrastes de couleurs de cette page
```

```
Analyse les formulaires de cette page pour la conformité RGAA
```

```
Est-ce que cette page a une bonne structure de navigation ? 
Vérifie les liens d'évitement, l'ordre de tabulation et les landmarks.
```

#### Audit interactif

Vous pouvez aussi demander à Claude de **tester des interactions** :

```
Clique sur le bouton "Menu" puis vérifie que le menu déroulant 
est accessible au clavier et a les bons attributs ARIA
```

```
Ouvre la modale de connexion et audite le formulaire qu'elle contient
```

```
Navigue vers la page Contact puis audite les formulaires
```

### Étape 4 : Comprendre le rapport

Claude génère un rapport avec cette structure pour chaque thématique :

```
## 🖼️ Thématique 1 : Images — 7/9 critères conformes

### ✅ Critère 1.1 — Alternative textuelle (Conforme)
Toutes les 12 images informatives ont un attribut alt non vide.

### ❌ Critère 1.2 — Images décoratives (Non conforme)
3 images décoratives n'ont pas alt="" :
  → <img src="decoration.svg"> dans le footer — Ajouter alt=""
  → <img src="wave-bg.png"> dans .hero — Ajouter aria-hidden="true"
  → <img src="dot.gif"> dans .separator — Ajouter role="presentation"

### ⚠️ Critère 1.3 — Pertinence des alternatives (À vérifier)
2 images ont un alt potentiellement non pertinent :
  → <img alt="image"> — Alt trop générique
  → <img alt="IMG_4532.jpg"> — Alt semble être un nom de fichier

### N/A Critère 1.4 — CAPTCHA
Aucun CAPTCHA détecté sur la page.
```

### Scénarios courants

<details>
<summary><strong>🔍 Auditer un site e-commerce</strong></summary>

```
Audite cette page produit sur :
1. Les images (alt des photos produit)
2. Les formulaires (sélecteur de taille, bouton panier)
3. Les contrastes (prix, badges promo)
4. La navigation (fil d'Ariane, filtres)
```

</details>

<details>
<summary><strong>🏛️ Auditer un site de service public</strong></summary>

```
Cette page est un site de service public soumis au RGAA.
Fais un audit complet des 13 thématiques et génère 
un rapport au format du RGAA pour la déclaration d'accessibilité.
```

</details>

<details>
<summary><strong>📱 Auditer la version mobile</strong></summary>

```
Redimensionne la fenêtre à 320px de large puis vérifie :
- Le reflow du contenu (critère 10.11)
- La taille des zones cliquables
- Les gestes tactiles et leurs alternatives (critère 13.10)
```

</details>

<details>
<summary><strong>♿ Vérification après corrections</strong></summary>

```
La dernière fois tu avais trouvé des problèmes de contraste 
sur les boutons et des labels manquants sur le formulaire.
Revérifie ces points spécifiques.
```

</details>

<br>

---

<br>

## 🔄 Combiner les deux méthodes

Pour un audit complet, la meilleure approche est de **combiner les deux méthodes** en trois phases :

```
  Phase 1 : Code source (Claude Code)
  ────────────────────────────────────
  → Scan systématique de tous les fichiers
  → Détection des patterns récurrents
  → Correction automatique du code
  → Couvre ce qui n'est pas encore en production

                    ↓

  Phase 2 : Navigateur (Claude in Chrome)
  ────────────────────────────────────────
  → Vérification du rendu réel
  → Test du contenu dynamique (JS, AJAX)
  → Test des interactions (modales, menus)
  → Vérification des contrastes calculés
  → Test du comportement au clavier

                    ↓

  Phase 3 : Tests manuels
  ────────────────────────
  → Test avec lecteur d'écran (NVDA, VoiceOver)
  → Navigation clavier complète
  → Vérification de la pertinence des contenus
  → Test avec des utilisateurs en situation de handicap
```

### Exemple de workflow complet

```bash
# 1. Dans Claude Code : scan du code source
claude
> Fais un audit RGAA de tous les fichiers dans src/ 
> et génère un rapport dans docs/audit-rgaa.md

# 2. Corriger les problèmes détectés dans le code
> Corrige tous les problèmes critiques que tu as trouvés

# 3. Déployer en staging, puis dans Chrome :
# Ouvrir https://staging.mon-site.fr

# 4. Dans Claude in Chrome : vérifier le rendu
> Audite cette page et compare avec le rapport docs/audit-rgaa.md.
> Est-ce que toutes les corrections sont effectives ?

# 5. Tester les interactions
> Navigue dans le site en utilisant uniquement le clavier 
> et signale les problèmes
```

<br>

---

<br>

## 📊 Aide-mémoire des prompts

### Claude Code (code source)

| Besoin | Prompt |
|:---|:---|
| Audit complet | `Audit RGAA complet de src/` |
| Un seul fichier | `Vérifie l'accessibilité de src/pages/index.html` |
| Une thématique | `Vérifie les contrastes dans les fichiers CSS` |
| Correction auto | `Corrige les problèmes d'accessibilité trouvés` |
| Rapport | `Génère un rapport RGAA au format markdown` |
| Diff/PR | `Audite les changements de cette PR` |

### Claude in Chrome (navigateur)

| Besoin | Prompt |
|:---|:---|
| Audit complet | `Audit RGAA complet de cette page` |
| Une thématique | `Vérifie les formulaires de cette page` |
| Interaction | `Ouvre le menu et vérifie son accessibilité` |
| Mobile | `Teste le reflow à 320px` |
| Clavier | `Navigue au clavier et signale les problèmes` |
| Re-vérification | `Revérifie les contrastes après correction` |

<br>

---

<br>

## ❓ FAQ

<details>
<summary><strong>Les skills fonctionnent-ils avec des frameworks (React, Vue, Svelte, Astro) ?</strong></summary>

**Oui.** En mode Claude Code, les skills analysent le markup généré (JSX, templates Vue, etc.) et comprennent les patterns des frameworks. En mode Chrome, ils analysent le DOM rendu, donc le framework n'a aucune importance — c'est le HTML final qui compte.

</details>

<details>
<summary><strong>Peut-on auditer un site en anglais ou dans une autre langue ?</strong></summary>

**Oui.** Les critères RGAA sont universels (basés sur WCAG 2.1). La seule différence est le critère 8.4 (validité du code de langue) qui vérifiera que l'attribut `lang` correspond bien à la langue réelle du contenu.

</details>

<details>
<summary><strong>Les skills remplacent-ils un audit RGAA officiel ?</strong></summary>

**Non.** Un audit RGAA officiel nécessite un expert certifié, des tests avec technologies d'assistance, et un échantillon représentatif de pages. Ces skills sont un **outil d'aide** qui accélère la détection des non-conformités, mais ne remplacent pas l'expertise humaine ni les tests utilisateurs.

</details>

<details>
<summary><strong>Quelle est la différence avec axe DevTools ou WAVE ?</strong></summary>

Les outils comme axe et WAVE appliquent des règles fixes sur le DOM. Les skills RGAA apportent trois avantages :

1. **Couverture RGAA spécifique** — les règles sont mappées exactement sur les 106 critères du RGAA, pas sur les WCAG génériques
2. **Jugement contextuel** — Claude peut analyser si un alt text est pertinent dans son contexte, pas juste vérifier qu'il existe
3. **Correction intégrée** — en mode Claude Code, Claude peut directement corriger le code source

En revanche, axe et WAVE sont plus rapides pour un scan automatique pur et s'intègrent mieux dans les pipelines CI/CD existantes.

</details>

<details>
<summary><strong>Comment gérer les contenus dynamiques (SPA, AJAX) ?</strong></summary>

En mode Claude in Chrome, demandez à Claude d'interagir avec la page avant l'audit :

```
Clique sur l'onglet "Tarifs", attends que le contenu charge, 
puis audite la section qui s'affiche
```

En mode Claude Code, analysez les composants qui génèrent le contenu dynamique directement dans le code source.

</details>

<details>
<summary><strong>Quel est le périmètre d'un audit ? Une page ou un site entier ?</strong></summary>

**Chaque audit porte sur une seule page** (ou un ensemble de fichiers en mode Claude Code). Pour un audit de site complet conforme au RGAA, il faut auditer un échantillon représentatif de pages — typiquement la page d'accueil, une page de contenu, une page de formulaire, la page de contact, les mentions légales, et les principales pages fonctionnelles.

En mode Claude in Chrome, relancez l'audit sur chaque page. En mode Claude Code, vous pouvez scanner plusieurs fichiers en une seule passe.

</details>

<details>
<summary><strong>Comment obtenir un score de conformité global ?</strong></summary>

Demandez à Claude de synthétiser les résultats :

```
Fais un audit RGAA complet et calcule le taux de conformité 
selon la méthode officielle du RGAA 
(nombre de critères conformes / nombre de critères applicables × 100).
```

Le RGAA définit trois niveaux : non conforme (< 50 %), partiellement conforme (50-99 %), totalement conforme (100 %).

</details>

<br>

---

<p align="center">
  <sub>← Retour au <a href="README.md">README</a></sub>
</p>

<p align="center">
  <strong>♿ L'accessibilité n'est pas une fonctionnalité. C'est un droit fondamental.</strong>
</p>
