---
supportType: "slide"
---

# Theme & Child Theme

<section class="slides">
<section class="slide">
  <div class="slide-inner">

## Thème

- la présentation du site
- un repertoire dans wp-content/themes
- un seul thème peut être activé
- un site n’existe pas sans thème

  </div>
</section>

<section>
<div>

## Architecture d'un thème

peut varier mais contient des éléments :

## fichier `style.css`

Un papier d’identité d’un thème + les styles

### fichier `functions.php`

Un cerveau du thème, écrit en PHP

### fichiers templates (modèles)

- `page.php`
- `single.php`
- `index.php`
  …

un mixte de php (fonctions de WordPress) et html + appels aux fichiers _“sous-templates”_

</div>
</section>
</section>
