---
supportType: "normal"
title: "Gatsby"
---

## API REST de WordPress

WordPress vient avec une API REST

L'endpoints commencent par `/wp-json/wp/v2/` par exemple `/wp-json/wp/v2/posts/` ou `/wp-json/wp/v2/pages/`

https://codepen.io/pehaa/pen/bb1a89259e3e7412781dc412834261bb

## Vous allons pourtant utiliser GraphQL

https://www.technologies-ebusiness.com/enjeux-et-tendances/graphql-approche-api-rest

Pour ceci nous allons installer un plugin WordPress `WPGraphQL`

## WordPress avec Gatsby

Installation :

```bash
npm add -g gatsby-cli
```

Ensuite nous allons démarrer un projet WordPress

```bash

```

`http://localhost:8000`

`http://localhost:8000/__graphql`

### Utilisation de static queries

Vous pouvez utiliser une _static query_ (query sans variables) dans vos components, voici un exemple qui permet de mettre en place la tagline du site

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
