---
supportType: "normal"
title: "Traductions"
---

# 🇫🇷Traductions

## Introduction théorique

Dans l’informatique, le système _gettext_ permet de séparer la programmation de la traduction.

Comment _gettext_ fonctionne ?

Au cours de la programmation, toutes les chaînes de caractères qui devraient être traduites sont marqués de façon spéciale, par exemple `__( "I should be translated", "project-text-domain" )`.  


Un site WordPress est composé de plusieurs “projets” (thème et plusieurs extensions), `"project-text-domain"` permet de traiter les textes de chaque thème et extension séparément.  
  
✅ Dans notre cas, le *text domain* est `"astra-child-simplon"` et nous mettons tous nos textes ainsi : `__( "I should be translated", "astra-child-simplon" )`  
  
---
  
👉 Premièrement, un fichier modèle (template, fichier `POT`) est créé. Ce fichier aura l’extension `.pot` (*Portable Object Template*). Il comprendra tous les chaines   de caractères à traduire, extraites de tous les fichiers au sein d’un projet.  

![](https://wptemplates.pehaa.com/assets/pot.png)
  
---
  
👉 Le fichier POT sera utilisé pour créer les fichier `.po` (*Portable Object*) pour chaque langue de traduction (par exemple `fr_FR.po`, `de_DE.po`, etc.)  
  
---
  
Le fichiers `.po` sont compilés en fichiers binaires `.mo` (*Machine Object*)  
  
---
  
Les fichiers `.mo` sont utilisés par WordPress pour assembler le document HTML selon la langue du site.  
  

## Loco Translate

Afin de générer le fichier `.POT` et ensuite les fichiers `.po` et `.mo` pour la langue française, nous allons utiliser une extension WordPress Loco Translate.

![](https://paper-attachments.dropbox.com/s_F45F85F9387024D6F24B7C73EA6CDAAB2433290EEB9CB765965C08123927E256_1608015360101_Loco+Translate.png)


Ensuite, dans Themes, nous allons choisir “Astra Child Simplon” et clicker “Créer un modèle” - nous allons ainsi générer le fichier POT.

![](https://wptemplates.pehaa.com/assets/create-pot.png)


Une fois fichier POT créé, nous allons ajouter une nouvelle langue (Dans Themes > Astra Child Simplon cliquer Nouvelle langue)


Une fois le bouton “Save” appuyé la traduction des chaines de caractères des fichiers .php est prise en compte.
