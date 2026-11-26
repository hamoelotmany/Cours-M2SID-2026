# Guide d'installation et d'initiation à RStudio & R Markdown (`knitr`)

Ce guide vous accompagne pas à pas pour installer l'environnement de travail (**R** et **RStudio**), découvrir l'interface et configurer **R Markdown / `knitr`** afin d'exécuter et compiler les fichiers `.Rmd` des travaux pratiques.

---

## 1. Installation de R et RStudio

> **Important :** Installez toujours **R** en premier, puis **RStudio** ensuite.

### Étape 1 : Installer R (le moteur de calcul)
1. Rendez-vous sur le site officiel du CRAN : [https://cran.r-project.org/](https://cran.r-project.org/)
2. Cliquez sur le lien correspondant à votre système d'exploitation :
   * **Windows** : cliquez sur *base*, puis sur *Download R-4.x.x for Windows* et lancez l'installateur (conservez les options par défaut).
   * **macOS** : choisissez le fichier `.pkg` adapté à votre processeur (*Apple silicon M1/M2/M3/M4* ou *Intel*).
   * **Linux (Ubuntu/Debian)** : exécutez dans votre terminal `sudo apt update && sudo apt install r-base`.

### Étape 2 : Installer RStudio Desktop (l'interface de travail)
1. Rendez-vous sur le site de Posit : [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)
2. Descendez jusqu'à la section **2: Install RStudio** et téléchargez la version recommandée pour votre ordinateur.
3. Lancez l'installation en gardant les paramètres par défaut.
4. Une fois terminé, **ouvrez uniquement RStudio** (inutile d'ouvrir R séparément).

---

## 2. Initiation rapide à RStudio

Au démarrage, l'interface de RStudio se divise en **4 panneaux principaux** :

1. **Éditeur de scripts / Documents (en haut à gauche)** : Zone où vous rédigez et modifiez vos fichiers `.R` ou `.Rmd`. *(Si ce panneau n'est pas visible, cliquez sur `File > New File > R Script` ou ouvrez un fichier existant).*
2. **Console (en bas à gauche)** : Zone où R exécute les commandes et affiche les résultats numériques ou les messages d'erreur.
3. **Environnement / Historique (en haut à droite)** : Liste les jeux de données, variables et modèles actuellement chargés en mémoire.
4. **Fichiers / Graphiques / Packages / Aide (en bas à droite)** :
   * *Files* : Explorateur de fichiers de votre ordinateur.
   * *Plots* : Affichage des graphiques générés.
   * *Packages* : Gestionnaire des extensions installées.
   * *Help* : Documentation officielle des fonctions R (accessible aussi en tapant `?nom_fonction` dans la console).

### Bonne pratique : Utiliser un Projet RStudio (`.Rproj`)
Pour éviter les problèmes de chemins de fichiers lors de l'importation des données :
1. Placez votre script `.Rmd` et vos fichiers de données (`.csv`, `.txt`) dans un même dossier.
2. Dans RStudio, cliquez en haut à droite sur **Project: (None) > New Project... > Existing Directory**, sélectionnez votre dossier et cliquez sur **Create Project**.

---

## 3. Installation des packages pour R Markdown (`knitr`)

Pour compiler un fichier `.Rmd` en document HTML ou PDF, R utilise les packages **`rmarkdown`** et **`knitr`**.

1. Dans RStudio, cliquez dans le panneau **Console** (en bas à gauche).
2. Copiez-collez la commande suivante et appuyez sur **Entrée** :

```r
install.packages(c("rmarkdown", "knitr"))
```

### Optionnel : Activer l'export au format PDF
Si vous souhaitez compiler vos comptes-rendus directement en **PDF** (en plus du format HTML), installez la distribution LaTeX légère **`tinytex`** en exécutant ces deux lignes dans la Console :

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

---

## 4. Exécuter et compiler un fichier `.Rmd` avec `Knit`

Un fichier **R Markdown (`.Rmd`)** combine du texte rédigé en Markdown et des blocs de code R (*chunks*).

### Structure d'un fichier `.Rmd`
* **En-tête YAML (en haut, entre `---`)** : Définit le titre, l'auteur, la date et le format de sortie (`html_document` ou `pdf_document`).
* **Zone de texte** : Vos explications, hypothèses et interprétations statistiques.
* **Blocs de code R (*chunks*)** : Délimités par ```` ```{r} ```` et ```` ``` ````.

### Comment exécuter le code et générer le rapport ?
1. **Ouvrir le fichier** : Dans RStudio, allez dans `File > Open File...` et sélectionnez votre fichier `.Rmd`.
2. **Tester bloc par bloc** : Cliquez sur la petite **flèche verte (▶)** en haut à droite d'un bloc de code pour exécuter uniquement ce bloc et vérifier vos résultats.
3. **Compiler tout le document (`Knit`)** :
   * Cliquez sur le bouton **Knit** (icône avec une pelote de laine) situé dans la barre d'outils au-dessus de l'éditeur.
   * *(Vous pouvez cliquer sur la petite flèche à côté de **Knit** pour choisir entre **Knit to HTML** ou **Knit to PDF**).*
   * RStudio exécute l'ensemble du code dans un environnement propre et génère automatiquement le fichier final dans le même dossier que votre `.Rmd`.

---

## 5. Résolution des erreurs fréquentes lors du `Knit`

| Problème rencontré | Cause probable | Solution |
| :--- | :--- | :--- |
| `Error: object 'x' not found` | Une variable a été créée dans votre console mais pas dans le fichier `.Rmd`. | Assurez-vous que toutes les étapes (importation des données, créations de variables) figurent bien dans les blocs de code du `.Rmd`, dans l'ordre chronologique. |
| `Error in library(...) : there is no package called '...'` | Un package utilisé n'est pas encore installé sur votre machine. | Installez-le via `install.packages("nom_du_package")` dans la console, **puis supprimez** la ligne `install.packages(...)` de votre fichier `.Rmd`. |
| `Error: cannot open file 'data.csv'` | Le fichier de données n'est pas dans le même dossier que le `.Rmd`. | Placez le jeu de données et le fichier `.Rmd` dans le même dossier et utilisez uniquement le nom du fichier (`read.csv("data.csv")`). |

