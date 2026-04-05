<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://img.shields.io/badge/%E2%99%BF-RGAA_Audit_Skills-8B5CF6?style=for-the-badge&labelColor=1a1a2e&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjxwYXRoIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0wIDE4Yy00LjQyIDAtOC0zLjU4LTgtOHMzLjU4LTggOC04IDggMy41OCA4IDgtMy41OCA4LTggOHoiLz48L3N2Zz4=">
    <img alt="RGAA Audit Skills" src="https://img.shields.io/badge/%E2%99%BF-RGAA_Audit_Skills-8B5CF6?style=for-the-badge&labelColor=1a1a2e">
  </picture>
</p>

<h1 align="center">Skills d'Audit d'Accessibilité RGAA</h1>

<p align="center">
  <strong>13 skills Claude pour auditer l'accessibilité de vos sites web selon le RGAA v4.1.2 (WCAG 2.1 AA).<br>Fonctionne sur le code source (Claude Code) et sur les sites en ligne (Claude in Chrome).</strong>
</p>

<p align="center">
  <a href="#-démarrage-rapide"><img src="https://img.shields.io/badge/Démarrage_rapide-→-10B981?style=flat-square" alt="Démarrage rapide"></a>
  <a href="#-les-13-thématiques"><img src="https://img.shields.io/badge/13_Thématiques-106_Critères-3B82F6?style=flat-square" alt="106 Critères"></a>
  <a href="TUTORIAL.md"><img src="https://img.shields.io/badge/Tutoriel_complet-→-F59E0B?style=flat-square" alt="Tutoriel"></a>
  <a href="https://accessibilite.numerique.gouv.fr/methode/criteres-et-tests/"><img src="https://img.shields.io/badge/RGAA-v4.1.2-EF4444?style=flat-square" alt="RGAA v4.1.2"></a>
</p>

<br>

<p align="center">
  <img src="https://img.shields.io/badge/WCAG_2.1-Niveau_AA-success?style=flat-square&logo=w3c&logoColor=white" alt="WCAG 2.1 AA">
  <img src="https://img.shields.io/badge/EN_301_549-V2.1.2-blue?style=flat-square" alt="EN 301 549">
  <img src="https://img.shields.io/badge/Licence-MIT-yellow?style=flat-square" alt="Licence MIT">
</p>

---

<br>

## Le problème

> **Plus de 96 % des pages d'accueil présentent des erreurs d'accessibilité détectables.** — [WebAIM Million, 2024](https://webaim.org/projects/million/)

Auditer l'accessibilité d'un site, c'est long, technique et fastidieux. Le RGAA définit **106 critères** répartis en 13 thématiques — et les vérifier un par un, page par page, relève du parcours du combattant.

**Ces skills automatisent le gros du travail.** Ils extraient les éléments pertinents, calculent les rapports de contraste, vérifient les attributs ARIA, valident la hiérarchie des titres et signalent les non-conformités — puis produisent un rapport d'audit structuré et actionnable.

<br>

## ✨ Démarrage rapide

Ces skills fonctionnent dans **deux contextes** selon votre situation :

### 🖥️ Vous avez le code source → Claude Code

```bash
# Installer les skills
for skill in dist/*.skill; do claude install-skill "$skill"; done

# Ouvrir votre projet et lancer un audit
cd /chemin/vers/mon-projet && claude
> Audite l'accessibilité RGAA de src/pages/index.html
```

Claude analyse vos fichiers et peut **corriger le code directement**.

### 🌐 Vous avez juste l'URL → Claude in Chrome

1. Installez les fichiers `.skill` dans **Paramètres → Skills** de Claude
2. Ouvrez le site à auditer dans Chrome
3. Demandez à Claude :

```
Audite cette page sur l'accessibilité des formulaires
```

Claude inspecte le DOM rendu en temps réel et retourne un rapport de conformité.

<br>

> 📖 **Instructions détaillées, exemples par thématique et scénarios avancés → [Tutoriel complet](TUTORIAL.md)**

<br>

## 📋 Les 13 thématiques

| | Thématique | Fichier | Critères | Ce qui est vérifié |
|:---:|:---|:---|:---:|:---|
| 🖼️ | **Images** | `rgaa-images.skill` | 9 | Alternatives textuelles, images décoratives, CAPTCHA, descriptions détaillées, images textes, figure/figcaption |
| 🪟 | **Cadres** | `rgaa-frames.skill` | 2 | Présence et pertinence du `title` sur les iframe/frame |
| 🎨 | **Couleurs** | `rgaa-colors.skill` | 3 | Information par la couleur seule, contraste texte (4.5:1 / 3:1), contraste composants d'interface (3:1) |
| 🎬 | **Multimédia** | `rgaa-multimedia.skill` | 13 | Transcriptions, sous-titres, audiodescription, contrôle du son automatique, commandes clavier |
| 📊 | **Tableaux** | `rgaa-tables.skill` | 8 | En-têtes et scope, résumés, titres, restrictions des tableaux de mise en forme |
| 🔗 | **Liens** | `rgaa-links.skill` | 2 | Intitulé explicite, nom accessible non vide, détection des textes génériques |
| ⚡ | **Scripts** | `rgaa-scripts.skill` | 5 | Rôles/états/propriétés ARIA, contrôle au clavier, régions live, changements de contexte |
| 📄 | **Éléments obligatoires** | `rgaa-mandatory-elements.skill` | 10 | Doctype, `lang`, titre de page, validité HTML, balisage sémantique, sens de lecture |
| 🏗️ | **Structuration** | `rgaa-information-structure.skill` | 4 | Hiérarchie des titres, landmarks, balisage des listes et des citations |
| 🎯 | **Présentation** | `rgaa-information-presentation.skill` | 14 | CSS, zoom 200%, focus visible, reflow 320px, espacement du texte, contenus au survol/focus |
| 📝 | **Formulaires** | `rgaa-forms.skill` | 13 | Étiquettes, regroupement de champs, validation, messages d'erreur, autocomplete |
| 🧭 | **Navigation** | `rgaa-navigation.skill` | 11 | Liens d'évitement, tabulation, pièges au clavier, plan du site, cohérence des menus |
| 👁️ | **Consultation** | `rgaa-consultation.skill` | 12 | Limites de temps, nouvelles fenêtres, documents bureautiques, clignotements, orientation, gestes |

**Total : 106 critères** couvrant l'intégralité du RGAA v4.1.2.

<br>

## 🔍 Comment ça marche

```
  1. EXTRAIRE              2. ÉVALUER               3. RAPPORTER

  ┌───────────┐           ┌───────────┐            ┌───────────┐
  │ Collecter │──────────▶│ Appliquer │───────────▶│ Générer   │
  │ éléments  │           │ critères  │            │ rapport   │
  │ HTML/ARIA │           │ RGAA      │            │ d'audit   │
  └───────────┘           └───────────┘            └───────────┘

  Code source ou DOM       Tests automatisés        ✅ ❌ ⚠️ N/A
  rendu en temps réel      + points à vérifier      + recommandations
                           manuellement
```

Les skills distinguent clairement ce qui est **entièrement automatisable** (alt manquant, contraste insuffisant, label absent, id dupliqué) de ce qui **nécessite un jugement humain** (pertinence d'un texte alternatif, qualité de l'organisation du contenu).

<br>

## 📖 À propos du RGAA

Le **Référentiel Général d'Amélioration de l'Accessibilité** (RGAA) est le référentiel technique de l'État français, basé sur les **WCAG 2.1 niveau AA** et la norme européenne **EN 301 549 V2.1.2**.

Il est **juridiquement obligatoire** pour les organisations publiques, les délégataires de service public et les entreprises privées de plus de 250 M€ de chiffre d'affaires annuel. Version en vigueur : 4.1.2 (décembre 2023).

→ [Documentation officielle du RGAA](https://accessibilite.numerique.gouv.fr/)

<br>

## ⚠️ Limites

Ces skills sont des **assistants d'audit**, pas un remplacement de l'expertise humaine. Les outils automatisés détectent environ 30 à 40 % des problèmes d'accessibilité. Ils constituent un excellent premier balayage, mais doivent être complétés par des tests avec lecteurs d'écran (NVDA, JAWS, VoiceOver), une navigation clavier complète, et idéalement des tests avec des utilisateurs en situation de handicap.

> Voir la [FAQ du tutoriel](TUTORIAL.md#-faq) pour plus de détails sur les limites et comment les contourner.

<br>

## 📁 Structure du dépôt

```
rgaa-accessibility-audit/
├── README.md                ← Vous êtes ici
├── TUTORIAL.md              ← Guide d'utilisation détaillé
├── LICENSE
├── skills/                  ← Code source des 13 skills
│   ├── rgaa-images/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── criteria.md
│   ├── rgaa-frames/
│   ├── rgaa-colors/
│   ├── rgaa-multimedia/
│   ├── rgaa-tables/
│   ├── rgaa-links/
│   ├── rgaa-scripts/
│   ├── rgaa-mandatory-elements/
│   ├── rgaa-information-structure/
│   ├── rgaa-information-presentation/
│   ├── rgaa-forms/
│   ├── rgaa-navigation/
│   └── rgaa-consultation/
└── dist/                    ← Fichiers .skill prêts à installer
    └── *.skill
```

<br>

## 🤝 Contribuer

1. **Signaler les faux positifs/négatifs** — ouvrez une issue avec l'URL et le résultat attendu
2. **Améliorer les scripts de détection** — les snippets JavaScript peuvent toujours être plus robustes
3. **Ajouter des fichiers de référence** — seule la thématique Images a un `references/criteria.md` détaillé
4. **Traduire les skills** — les SKILL.md sont en anglais, des versions françaises seraient utiles

<br>

## 📄 Licence

MIT — utilisez librement, auditez, rendez le web accessible.

<br>

---

<p align="center">
  <sub>Construit à partir de la spécification officielle <a href="https://accessibilite.numerique.gouv.fr/methode/criteres-et-tests/">RGAA v4.1.2</a> de la Direction interministérielle du numérique.</sub>
</p>

<p align="center">
  <strong>♿ Le web devrait être accessible à tous.</strong>
</p>
