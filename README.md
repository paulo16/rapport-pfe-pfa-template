# Template Rapport PFA/PFE — ISMAGI

Structure LaTeX prête à l'emploi pour rédiger un rapport de Projet de Fin d'Année.
Consultez également le fichier `guide-latex-pfa.tex` pour un cours complet sur LaTeX.

---

## Installation (à faire une seule fois)

### Option A — VS Code (recommandé)

**1. Installer MiKTeX** (le compilateur LaTeX)
- Télécharger sur : https://miktex.org/download
- Choisir **Windows 64-bit**
- Durant l'installation, cocher **"Install missing packages automatically"**
- Redémarrer le PC après installation

**2. Installer VS Code** (l'éditeur)
- Télécharger sur : https://code.visualstudio.com

**3. Installer l'extension LaTeX Workshop dans VS Code**
- Ouvrir VS Code → `Ctrl+Shift+X` → chercher **LaTeX Workshop** (par James Yu) → Installer

**4. Configurer LaTeX Workshop pour utiliser pdflatex** (important — évite l'erreur Perl)

Ouvrir les settings JSON (`Ctrl+Shift+P` → *Open User Settings JSON*) et ajouter :

```json
"latex-workshop.latex.recipes": [
    {
        "name": "pdflatex",
        "tools": ["pdflatex"]
    },
    {
        "name": "pdflatex -> bibtex -> pdflatex x2",
        "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
    }
],
"latex-workshop.latex.tools": [
    {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ]
    },
    {
        "name": "bibtex",
        "command": "bibtex",
        "args": ["%DOCFILE%"]
    }
],
"latex-workshop.latex.recipe.default": "pdflatex",
"latex-workshop.view.pdf.viewer": "tab",
"latex-workshop.latex.autoBuild.run": "onSave"
```

---

### Option B — TeXmaker (plus simple pour débutants)

**1. Installer MiKTeX** (voir étape 1 ci-dessus)

**2. Installer TeXmaker**
- Télécharger sur : https://www.xm1math.net/texmaker/

**3. Définir le document maître**
- Ouvrir `main.tex` dans TeXmaker
- Menu **Options** → **Définir le document maître** → **Utiliser le document courant**

---

## Compiler le rapport

### Avec VS Code
- Ouvrir `main.tex`
- Appuyer sur `Ctrl+S` (le PDF se génère automatiquement)
- Ou `Ctrl+Alt+B` pour forcer la compilation

### Avec TeXmaker
- Ouvrir `main.tex`
- Appuyer sur **F6** (pdfLaTeX)
- Pour mettre à jour la bibliographie : F6 → F11 → F6 → F6

---

## Arborescence du projet

```
rapport-pfa-l2/
├── main.tex                  ← Point d'entrée (seul fichier à compiler)
├── preamble.tex              ← Packages et style global
├── guide-latex-pfa.tex       ← Cours LaTeX pour débutants
├── frontmatter/
│   ├── page-garde.tex
│   ├── remerciements.tex
│   ├── resume-fr.tex
│   ├── abstract-en.tex
│   └── liste-abreviations.tex
├── chapters/
│   ├── 00-introduction-generale.tex
│   ├── 01-contexte-etat-art.tex
│   ├── 02-analyse-besoins.tex
│   ├── 03-conception.tex
│   ├── 04-implementation.tex
│   ├── 05-tests-resultats.tex
│   └── 06-conclusion-perspectives.tex
├── appendices/
│   ├── annexe-a-cdc-detaille.tex
│   ├── annexe-b-guides-techniques.tex
│   └── annexe-c-code-complementaire.tex
├── bib/
│   └── references.bib        ← Références bibliographiques
└── images/
    ├── ch01/ à ch05/         ← Images par chapitre
    └── global/               ← Logo et images communes
```

---

## Erreurs fréquentes

| Erreur | Solution |
|--------|----------|
| `latexmk did not succeed — perl not found` | Suivre l'étape 4 de la configuration VS Code ci-dessus |
| `File not found` | Vous compilez un fichier fragment — ouvrir et compiler `main.tex` |
| `Fichier de log non trouvé` | MiKTeX n'est pas installé, ou `main.tex` n'est pas le document maître |
| Image introuvable | Vérifier le chemin dans `\includegraphics{}` — utiliser `.png` ou `.jpg` |
| Références `??` dans le PDF | Compiler deux fois, ou faire le cycle F6 → F11 → F6 → F6 |
