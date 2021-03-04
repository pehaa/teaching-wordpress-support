---
supportType: "normal"
title: "Sélecteurs CSS"
---

# Sélecteurs CSS

## Différents types de sélecteurs et comment les combiner ?

[Commandez tout ce qui vous plaît.](https://css-cantine.netlify.app/)

[![css cantine](https://wptemplates.pehaa.com/assets/alyra/css-cantine.png)](https://css-cantine.netlify.app/)

Playground sélecteurs :

https://codepen.io/alyra/pen/jOVxbLp

## Type Selector

`tag {}`

En français _sélecteur de type._ Les _sélecteurs de type_ ciblent des éléments en fonction du nom de leur balise (`tag`) HTML ou XML, comme `div`, `p`, `ul`, `assiette` etc. C'est un sélecteur simple.

```css
img {
  max-width: 100%;
  height: auto;
}
```

```css
body {
  background: lavender;
}
```

---

## Class Selector

`.class {}`

En français _sélecteur de classe._ Le symbole `.` suivi (sans espace) par le nom de la classe permet de cibler tous les éléments qui ont cette classe. C'est un sélecteur simple.

```css
.mini {
  font-size: 0.875rem;
}
```

---

## ID Selector

`#id`

En français _sélecteur d'identifiant._ Avec le symbole `#` suivi (sans espace) par le nom d'identifiant on peut cibler un élément par son attribut `id.` C'est un sélecteur simple.

```css
#top {
  position: fixed;
  top: 0;
}
```

---

## The Universal Selector

`* {}`

En français - sélecteur universel. Il correspond à un élément de n'importe quel type. C'est un sélecteur simple.

```css
* {
  box-sizing: border-box;
}
```

---

## Attribute selector

`[attr] {}`,  
`[attr=value] {}`,  
`[attr*=value] {}`,  
`[attr^=value] {}`,  
`[attr$=value] {}`,  
`[attr~=value] {}`

En français _sélecteur d'attribut._ C'est un sélecteur simple.

<dl>
 <dt><code class="language-text">[<em>attr</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code>.</dd>
 <dt><code class="language-text">[<em>attr</em>=<em>value</em>]</code></dt>
 <dd>Cible  des éléments avec l'attribut <code class="language-text">attr</code> dont la valeur est exactement <code class="language-text">value</code>.</dd>
 <dt><code class="language-text">[<em>attr</em>~=<em>value</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code> dont la valeur contient <code class="language-text">value</code> séparée par des espaces.
 <dt><code class="language-text">[<em>attr</em>|=<em>value</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code> dont la valeur est exactement <code class="language-text">value</code> ou dont la valeur commence par <code class="language-text">value</code> suivi immédiatement d'un tiret (U+002D). Souvent utilisé avec des codes de langues.</dd>
 <dt><code class="language-text">[<em>attr</em>^=<em>value</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code> dont la valeur commence par <code class="language-text">value</code>.</dd>
 <dt><code class="language-text">[<em>attr</em>$=<em>value</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code> dont la valeur se termine par <code class="language-text">value</code>.</dd>
 <dt><code class="language-text">[<em>attr</em>*=<em>value</em>]</code></dt>
 <dd>Cible des éléments avec l'attribut <code class="language-text">attr</code> et dont la valeur contient au moins une occurrence de&nbsp;<code class="language-text">value</code>.</dd>
</dl>

```css
[lang="en"] {
  font-family: italic;
}

a[href^="#"] {
  background-color: gold;
}

a[href$="alyra.fr"] {
  background-color: blue;
  color: white;
}
```

Il existe aussi le sélecteur _lang pseudo-class_ `:lang()`

```css
:lang(en) {
  font-family: italic;
}
```

---

## Descendant Combinator

`A B {}`

En français : le combinateur de descendance. Permet de combiner deux sélecteurs sous la forme `A B`.
`A B` cible des éléments qui correspondent au sélecteur `B` uniquement si ceux-ci ont un élément ancêtre qui correspond au premier sélecteur (`A`).
Attention à l'espace entre deux éléments.

```css
header p {
  font-weight: bold;
}
```

---

## Selector list (,)

`A, B {}`

Cibler en même temps les éléments `A` et `B`. On peut ainsi combiner plusieurs types de sélecteurs et en avoir plus de deux.

```css
h1,
h2,
h3,
.heading {
  font-family: Montserrat, sans-serif;
  font-weight: 900;
}
```

---

Dans les derniers cas ci-dessus, nous utilisons un espacement ou la virgule pour séparer les sélecteurs. Nous arrivons ainsi à combiner des sélecteurs simples.

Mais que se passe-t-il si deux sélecteurs simples sont collés ensemble ? Par exemple `p.mini` ou `#top.mini` ?

En collant des sélecteurs ensemble (sans espace) nous ajoutons des restrictions, `AB` cible des éléments qui correspondent en même temps au sélecteur `A` et `B`.

---

## Child Selector

`A > B {}`

Permet de combiner des sélecteurs. Cible les éléments `B` qui sont des enfants directs des éléments `A`.

```css
header > div {
  border: 3px solid;
}
```

---

## Adjacent Sibling Selector

`A + B {}`

Permet de combiner des sélecteurs. `A + B` cible tous les éléments `B` qui suivent directement les `A`.

```css
h2 + p {
  font-size: 0.875rem;
  text-transform: uppercase;
}
```

---

## General sibling combinator"

`A ~ B {}`

Permet de combiner des sélecteurs. A ~ B cible tous les éléments `B` qui suivent les `A`.

---

## First Child Pseudo-class

`:first-child {}`

Cible les éléments qui sont les premiers enfants de son élément parent.

```css
li:first-child {
  font-weight: bold;
}
```

---

## nth Child Pseudo-class

`:nth-child(..) {}`

Cible les éléments qui sont les enfants numéro .. de son élément parent.

```css
li:nth-child(2n + 1) {
  background: pink;
}
/*
li:nth-child(1) {
  background: pink;
}
li:nth-child(3) {
  background: pink;
}
li:nth-child(5) {
  background: pink;
}
...
*/
```

---

## Last Child Pseudo-class

`:last-child {}`

Cible les éléments qui sont les derniers enfants de son élément parent.

```css
section p:last-child {
  margin-bottom: 0;
}
```

## First-of-type Pseudo-class

`:first-of-type {}`

Cible les éléments qui sont les premiers enfants de leurs types

```css
section p:first-of-type {
  font-size: 1.25rem;
}
```

---

Il existe aussi `only-child`, `nth-last-child`, `last-of-type`, `nth-of-type`, `nth-last-of-type`, `only-of-type`

---

## :not() Pseudo-class

`:not(A) {}`

Utilise la négation pour cibler les éléments. Cible tous les éléments qui ne correspondent pas au sélecteur `A`.

```css
img:not([alt]) {
  border: 5px solid red;
}
```

---

## Autres sélecteurs

- `:root { }` - cible la racine du document (`html`)
- `:hover { }` - l'apparence d'un élément au survole
- `:focus { }` - l'apparence d'un élément au focus
- `:link { }` - permet de sélectionner les liens à l'intérieur d'éléments. Il sélectionnera tout lien n'ayant pas été visité
- `:visited { }` - permet de modifier l'aspect d'un lien après que l'utilisateur l'a visité
- `:empty { }`
- `:target { }`
- `:enabled { }`
- `:disabled { }`
- `:checked { }`
- `:default { }`
- `:valid { }`
- `:invalid { }`
- `:in-range { }`
- `:out-of-range { }`
- `:required { }`
- `:optional { }`
- `:read-only { }`
- `:read-write { }`
- `:right { }`
- `:left { }`

### Pseudo-éléments

- `:before { }` - crée un pseudo-élément qui sera le premier enfant de l'élément sélectionné. Il est souvent utilisé pour ajouter du contenu cosmétique à un élément, en utilisant la propriété CSS `content`.
- `:after { }` - crée un pseudo-élément qui sera le dernier enfant de l'élément sélectionné. Il est souvent utilisé pour ajouter du contenu cosmétique à un élément, en utilisant la propriété CSS `content`.
- `::selection { }` - cible une portion du document qui a été sélectionnée par l'utilisateur
- `:first-letter { }`
- `:first-line { }`

https://codepen.io/alyra/pen/RwrrpBO

[![Bien  vise ?](https://wptemplates.pehaa.com/assets/alyra/quiz-selectors1.png)](https://cdpn.io/alyra/debug/6f79149941afdce6945473428e1395ac)
[Quiz "Bien visé ?"](https://cdpn.io/alyra/debug/6f79149941afdce6945473428e1395ac)
