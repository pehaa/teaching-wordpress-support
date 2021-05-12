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

Sur le site WordPress nous devons installer 2 plugins :

- [`WPGraphQL`](https://www.wpgraphql.com/)
- [`WPGatsby`](https://wordpress.org/plugins/wp-gatsby/)

En local nous devons installer `gatsby-cli`

```bash
npm add -g gatsby-cli
```

Ensuite nous allons démarrer un projet WordPress

```bash
gatsby new my-wordpress-gatsby-site https://github.com/pehaa/my-wordpress-gatsby-site-simplon
```

`http://localhost:8000`

Ici vous pouvez "préparer" vos queries :
`http://localhost:8000/___graphql`

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
- Personnaliser la Bio
- Personnaliser le Footer
- Modifier les styles - pourquoi pas articles dans une grille ?  
   Vous pouvez écrire CSS ou installer et utiliser une librairie (Bootstrap par exemple)
- Modifier la typo (astuce - vous pouvez installer les typos avec le package [typefaces](https://www.npmjs.com/package/typefaces), ensuite il faudra les importer dans le fichier `gatsby-browser.js` (remplacer _Merriweather_ et _Montserrat_) et utiliser quelque part dans votre stylesheet)
- Ajouter un sidebar et des widgets - reproduire WordPress widgets avec React et GraphQL static query
  - Recent Posts
  - Tags
  - Categories
- Toute créativité est bienvenue !!! 😍

À rendre:

- lien vers repo GitHub
- line vers le site publié (Netlify)
- présentation du projet (10 minutes par binômes)

## Sass

Si vous préferez `sass` que `css`, installez le ainsi que le plugin `gatsby-plugin-sass`

```bash
npm install sass gatsby-plugin-sass
```

Ensuite ajouter `gatsby-plugin-sass` dans l'array des plugins dans le fichier `gatsby-config.js`

```js
// gatsby-config.js
/**
 * 👋 Hey there!
 * This file is the starting point for your new WordPress/Gatsby site! 🚀
 * For more information about what this file is and does, see
 * https://www.gatsbyjs.com/docs/gatsby-config/
 *
 */

module.exports = {
  /**
   * Adding plugins to this array adds them to your Gatsby site.
   *
   * Gatsby has a rich ecosystem of plugins.
   * If you need any more you can search here: https://www.gatsbyjs.com/plugins/
   */
  plugins: [
    `gatsby-plugin-sass`,
    {
      /**
       * First up is the WordPress source plugin that connects Gatsby
       * to your WordPress site.
       *
       * visit the plugin docs to learn more
       * https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-source-wordpress/README.md
       *
       */
      resolve: `gatsby-source-wordpress`, // <----- ICI
      options: {
        // the only required plugin option for WordPress is the GraphQL url.
        url:
          process.env.WPGRAPHQL_URL || `https://pehaa.xyz/gatsby-demo/graphql`,
      },
    },
    // ... comme avant
```

Changez l'extension de fichier `src/css/style.css` pour `src/css/style.scss` - vous pouvez y utiliser scss maintenant.

N'oubliez pas de modifier aussi le fichier `gatsby-browser`

```js
// gatsby-browser.js
// ...
// custom CSS styles
// avant import "./src/css/style.css"
import "./src/css/style.scss"
```

Redémarrez le serveur.

## Images statiques

Pour utiliser des images statiques (les images qui ne sont pas chargées depuis WordPress), ajoutez les dans le dossier `static`

Ensuite, dans n'importe quel components vous pouvez les utiliser comme ci-dessous :

```js
<img src="/nom-de-fichier-dans-le-dossier-static.jpg" alt="" />
```
