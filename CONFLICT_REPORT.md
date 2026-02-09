# Rapport du Conflit Git - Projet Équipe de France

## Résumé du Conflit

Un conflit de fusion (merge conflict) a été identifié dans l'historique du projet le **23 janvier 2026 à 16:34:00**.

## Détails du Conflit

### Commit de Fusion
- **SHA**: `ba871a302cd83d5fbfe567cdea6edb8330a563a9`
- **Auteur**: Teter24 (158817394+Teter24@users.noreply.github.com)
- **Date**: Vendredi 23 janvier 2026, 16:34:00 +0100
- **Message**: "Merge branch 'develop' into feature/1-header"
- **Lien GitHub**: https://github.com/Adprog7/Tp-Git/commit/ba871a302cd83d5fbfe567cdea6edb8330a563a9

### Branches Concernées
- **Branche source**: `develop` (commit parent: `fef8074` - Merge PR #10)
- **Branche destination**: `feature/1-header` (commit parent: `73bbcd9` - vers PR #11)

### Pull Requests Associées
- **PR #10**: [feature/2-footer](https://github.com/Adprog7/Tp-Git/pull/10) - Ajout du footer
- **PR #11**: [feature/1-header](https://github.com/Adprog7/Tp-Git/pull/11) - Ajout du header

### Fichier en Conflit
Le conflit s'est produit dans le fichier: **`pages/index.html`**

## Nature du Conflit

Le conflit est survenu parce que les deux branches ont modifié le même fichier `pages/index.html` de manière différente:

### Branche `feature/1-header` (73bbcd9)
Cette branche a ajouté:
- Un header avec navigation
- Logo de l'Équipe de France
- Menu de navigation (Accueil, Histoire, Contact)
- Métadonnées dans le `<head>` (titre, favicon, fonts Google)
- Liens vers `../css/styles.css`

### Branche `develop` (fef8074)
Cette branche a ajouté:
- Un footer complet avec plusieurs colonnes de liens
- Liens vers différentes sections (La sélection, L'équipe, Billetterie & Fans, Infos)
- Logo FFF dans le footer
- Lien vers `../css/footer.css`

## Résolution du Conflit

Le conflit a été résolu en **combinant les modifications des deux branches**:

1. **Header conservé** de la branche `feature/1-header`
2. **Footer ajouté** de la branche `develop`
3. **Les deux fichiers CSS** ont été inclus:
   - `../css/styles.css` (pour le header)
   - `../css/footer.css` (pour le footer)

### Code Final Après Résolution

Le fichier `pages/index.html` après résolution contient:
- Le `<head>` de la branche `feature/1-header` avec l'ajout du lien vers `footer.css`
- Le `<header>` complet de la branche `feature/1-header`
- Le `<footer>` complet de la branche `develop`

## Statistiques du Merge

D'après l'analyse du commit de merge:
- **Ajouts**: 274 lignes
- **Suppressions**: 1 ligne
- **Total de changements**: 275 lignes

### Fichiers Modifiés lors du Merge
1. `css/footer.css` - Ajouté (109 lignes)
2. `images/fff-logo.png` - Ajouté
3. `pages/club-history.html` - Modifié (58 lignes)
4. `pages/contact.html` - Modifié (58 lignes)
5. `pages/index.html` - Modifié (49 ajouts, 1 suppression)

## Visualisation du Conflit

```
                    ┌─────────────────────┐
                    │   Commit 7a85025    │
                    │  (Initial README)   │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │   Commit 49ba5a2    │
                    │  (Structure HTML)   │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │   Commit 8a4bec9    │
                    │  (Structure CSS)    │
                    └──────────┬──────────┘
                               │
                ┌──────────────┴──────────────┐
                │                             │
    ┌───────────▼──────────┐      ┌──────────▼──────────┐
    │   Commit 73bbcd9     │      │   Commit 3dcb808    │
    │ feature/1-header     │      │  develop (footer)   │
    │ [AJOUTE: header]     │      │  [AJOUTE: footer]   │
    │                      │      │                     │
    │ Modifié:             │      │ Modifié:            │
    │ - pages/index.html   │      │ - pages/index.html  │
    │   (header + nav)     │      │   (footer complet)  │
    │                      │      └──────────┬──────────┘
    │                      │                 │
    │                      │      ┌──────────▼──────────┐
    │                      │      │   Commit fef8074    │
    │                      │      │ Merge PR #10        │
    │                      │      └──────────┬──────────┘
    │                      │                 │
    └──────────────────────┼─────────────────┘
                           │
                           │   ⚠️ CONFLIT ICI ⚠️
                           │   index.html modifié
                           │   dans les deux branches
                           │
                ┌──────────▼──────────┐
                │   Commit ba871a3    │
                │  [RESOLUTION DU     │
                │   CONFLIT]          │
                │                     │
                │  Merge develop →    │
                │  feature/1-header   │
                │                     │
                │  Résultat:          │
                │  header + footer    │
                └─────────────────────┘
```

### Lignes en Conflit

Le conflit s'est produit dans la section `<head>` et `<body>` du fichier `pages/index.html`:

**Branche feature/1-header voulait:**
```html
<head>
    <title>Équipe de France</title>
    <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
    <header class="hero-header">
        <!-- contenu du header -->
    </header>
</body>
```

**Branche develop voulait:**
```html
<head>
    <title></title>
    <link rel="stylesheet" href="../css/footer.css">
</head>
<body>
    <footer class="footer-container">
        <!-- contenu du footer -->
    </footer>
</body>
```

**Résolution (les deux combinés):**
```html
<head>
    <title>Équipe de France</title>
    <link rel="stylesheet" href="../css/styles.css">
    <link rel="stylesheet" href="../css/footer.css">  ← Ajouté
</head>
<body>
    <header class="hero-header">
        <!-- contenu du header -->
    </header>
    
    <footer class="footer-container">  ← Ajouté
        <!-- contenu du footer -->
    </footer>
</body>
```

## Contexte du Projet

Ce conflit s'est produit pendant le développement initial du site web de l'Équipe de France, où deux fonctionnalités étaient développées en parallèle:
- **Issue #1**: Création du header
- **Issue #2**: Création du footer

Les deux équipes travaillaient sur le même fichier `index.html`, ce qui a naturellement conduit à un conflit lors de l'intégration.

## Conclusion

Le conflit a été résolu avec succès en fusionnant les deux ensembles de modifications. La résolution était appropriée car les changements des deux branches étaient complémentaires (header en haut, footer en bas) et ne se chevauchaient pas fonctionnellement.

---

**Généré le**: 9 février 2026
**Commit de référence**: ba871a302cd83d5fbfe567cdea6edb8330a563a9
