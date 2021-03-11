---
supportType: "normal"
title: "Child Theme & la barre Personalizer"
---



# Child Theme

Nous pouvons ajouter nos propres options via la panel Personnaliser, voici comment l'activer :


```php
  /* functions.php */
  add_action( 'customize_register', 'my_child_theme_add_stuff_to_customizer' );
  function my_child_theme_stuff_to_customizer( $wp_customize ) { /* .... */ }
```

Ensuite dans la fonction `my_child_theme_stuff_to_customizer` nous allons ajouter une notre propre section et notre propre champs qui permettent d'enregister nos propres règlages.


```php
function my_child_theme_add_stuff_to_customizer( $wp_customize ) {

  /* ici j'ajoute la section */
  $wp_customize->add_section(
    'my_child_theme_custom_section', /* section id */
    array(
      'title'       => 'Réglages de mon thème',
      'description' => 'Les options ajoutés via mon thème enfant',
    )
  );

  /* ici j'ajoute un setting, une entrée dans la base de donnée pour mon option */

  $wp_customize->add_setting(
    'my_child_theme_custom_setting',
    array(
      'default'           => '',
      'sanitize_callback' => 'wp_kses_post', /* ceci dépend du type de données */
    )
  );

  $wp_customize->add_control(
    'my_child_theme_custom_setting',
    array(
      'type'        => 'textarea', /* différents types sont disponible */
      'section'     => 'my_child_theme_custom_section', // Required, core or custom.
      'label'       => __( 'Mon option' ),
      'description' => __( 'Est sa description.' ),
    )
  );
}
```


`sanitize_callback` :

- `wp_kses_post` - filtre html
- 
- `esc_url_raw` - filtre un url

## "Consommer" l'option dans le template :

```php

<?php echo get_theme_mod(my_child_theme_custom_setting); ?>

```


