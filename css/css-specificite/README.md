---
supportType: "normal"
title: "Sélecteurs CSS - Résolution de conflits"
---

# Sélecteurs CSS - Résolution de conflits

Avec tous ces types de sélecteurs et la possibilité de les combiner, il est clair que les éléments peuvent être ciblés à plusieurs manières.

Les 2 règles principales sont :

1. Le CSS est lu de haute en bas, les déclarations qui suivent prennent le dessus sur les déclarations précédentes.

1. Nos déclarations prennent toujours le dessur sur le _user agent stylesheet_

Regardons ensemble cet exemple :

```html
<ul class="personnages">
  <li class="list-item">Stormtrooper</li>
  <li class="list-item">Boba Fett</li>
  <li class="list-item">Dark Vador</li>
  <li class="list-item">Empereur Palpatine</li>
</ul>
```

```css
.personnages li {
  color: red;
}
.list-item {
  color: green;
}
ul > li {
  color: blue;
}
```

À votre avis de quelles couleurs seront nos personnages ?

<dl style="font-size:20px">
  <dt>Puissance "0"</dt>
  <dd>Sélecteurs universels <em>universal selector</em> <code class="language-text">*</code></dd>
  <dt>Puissance "1"</dt>
  <dd>
  <em>type selectors</em> <code class="language-text">html</code>, <code class="language-text">body</code>, <code class="language-text">div</code>,  &hellip;<br>
  <em>pseudo-elements</em> <code class="language-text">:before</code>, <code class="language-text">:after</code>, &hellip;</dd>
  <dt>Puissance "10"</dt>
  <dd>
    classes <code class="language-text">.title</code><br>
    attributs <code class="language-text">[class]</code>, <code class="language-text">[id]</code>, <code class="language-text">[title]</code>, <code class="language-text">[href]</code>, &hellip;<br>
    pseudo-classes <code class="language-text">:hover</code>, <code class="language-text">:first-child</code>, <code class="language-text">:lang()</code>, <code class="language-text">:focus</code>, &hellip;<br>
  </dd>
  <dt>Puissance "100"</dt>
  <dd>ids <code class="language-text">#top</code>, <code class="language-text">#contact</code>,</dd>
  <dt>Puissance "1000"</dt>
  <dd> <code class="language-text">style="font-weight:bold"</code> </dd>
  <dt>Puissance "10000"</dt>
  <dd><code class="language-text">{color: red!important;}</code></dd>
</dl>

[![La grille de spécificité en format .pdf](https://wptemplates.pehaa.com/assets/alyra/grille-specificite.png)](https://assets.codepen.io/4515922/Tableau_de_cartes%402x.pdf)

[![Specificity calculator](https://wptemplates.pehaa.com/assets/alyra/calculator.png)](https://specificity.keegan.st/)

![](https://wptemplates.pehaa.com/assets/alyra/mando.jpg)

> Des surspécificités, tu te méfieras… Plus efficaces les sélecteurs de base sont, pour qui sait les manipuler… Plus séducteur est le côté obscur, plus facile… N’en crois rien.

## Ex. 1

https://codepen.io/alyra/pen/MWKaXjG

## Ex. 2

https://codepen.io/alyra/pen/NWxGzbv

[Quizzzzz :](https://cdpn.io/alyra/debug/d341e5aba9eb51c6b9b0f517b45cf812)
[![](https://wptemplates.pehaa.com/assets/alyra/quiz-selectors2.png)](https://cdpn.io/alyra/debug/d341e5aba9eb51c6b9b0f517b45cf812)

[et l'affrontement final :](https://codepen.io/pehaa/debug/dEpvXN)
[![](https://wptemplates.pehaa.com/assets/alyra/quiz-selectors3.png)](https://codepen.io/pehaa/debug/dEpvXN)
