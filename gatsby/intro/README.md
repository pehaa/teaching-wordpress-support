---
supportType: "normal"
title: "Gatsby"
---

## API REST de WordPress

WordPress vient avec une API REST

L'API utilise le route `/wp-json/`. Les endpoints commencent par `/wp/v2/` par exemple :

- `/wp-json/wp/v2/posts/`
- `/wp-json/wp/v2/pages/`
- `/wp-json/wp/v2/categories`

https://codepen.io/pehaa/pen/bb1a89259e3e7412781dc412834261bb

## Vous allons pourtant utiliser GraphQL

GraphQL est une alternative à REST API. C'est un language de queries et un runtime:

- un seul endpoint
- deux opérations: query et mutation (pour modifier les données)
- retourne uniquement les champs demandés (optimisation en volumetrie des données)
- permet de _fetch_ plusieurs ressources dans une seule requête

[GRAPHQL : UNE APPROCHE API PAS EN REST](https://www.technologies-ebusiness.com/enjeux-et-tendances/graphql-approche-api-rest)
[GraphQL - documentation officielle](https://graphql.org/learn/)

Afin d'utiliser GraphQL avec WordPress nous allons installer un plugin WordPress [`WPGraphQL`](https://www.wpgraphql.com/)

https://codepen.io/pehaa/pen/0dd3b8c19b79edfdfeaa8a5e7419faa2

https://codepen.io/pehaa/pen/zYZvwEG

## WordPress avec Gatsby Framework

Installation :

```bash
npm add -g gatsby-cli
```

Ensuite nous allons démarrer un projet WordPress

```bash
gatsby new my-wordpress-gatsby-site https://github.com/pehaa/my-wordpress-gatsby-site-simplon
```

`http://localhost:8000`

`http://localhost:8000/__graphql`

### Utilisation de static queries

Vous pouvez utiliser une _static query_ (query sans variables) dans vos components, voici un exemple qui permet de mettre en place la tagline du site

#### Title & description

```js
// header.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby"
const Header = () => {
  const data = useStaticQuery(graphql`
    query LayoutQuery {
      wp {
        generalSettings {
          title
          description
        }
      }
    }
  `)
  const title = data.wp.generalSettings.title
  const description = data.wp.generalSettings.description
  return (
    <h1>{title}</h1>
    <p>{description}</p>
  )
}
export default Header
```

#### Navigation

Voici comment nous pouvons mettre en place la navigation

```js
// src/components/navigation.js
import React from "react"
import { Link, useStaticQuery, graphql } from "gatsby"

const Navigation = () => {
  const data = useStaticQuery(graphql`
    query MyQuery {
      wpMenu(name: { eq: "main" }) {
        menuItems {
          nodes {
            url
            label
            id
          }
        }
      }
    }
  `)
  const menu = data.wpMenu.menuItems.nodes
  return (
    <nav>
      {menu.map((el) => (
        <Link key={el.id} to={el.url}>
          {el.label}
        </Link>
      ))}
    </nav>
  )
}

export default Navigation
```

## Todos :

Soyez créatif, allez si loin que vous pouvez avec ce projet!

- Navigation
- Tagline
- Widgets - reproduire WordPress widgets avec React et GraphQL static query
  - Recent Posts
  - Tags
  - Categories
- Personnaliser la Bio
- Personnaliser le Footer
- Modifier les style - pourquoi pas articles dans une grille ? Vous pouvez écrire CSS ou installer et utiliser une librairie (Bootstrap par exemple)

A rendre:

- lien vers repo GitHub
- line vers le site publié (Netlify)
