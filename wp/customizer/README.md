---
supportType: "normal"
title: "WP Customizer"
---



# Child Theme & WP Customizer

![](https://wptemplates.pehaa.com/assets/brioche-cannelle-customizer.png)

Nous pouvons ajouter **nos propres options** via la panel _Personnaliser._  Voici comment l'activer :


```php
  /* functions.php */
  add_action( 'customize_register', 'my_child_theme_add_stuff_to_customizer' );
  function my_child_theme_stuff_to_customizer( $wp_customize ) { /* .... */ }
```

Ensuite dans la fonction `my_child_theme_add_stuff_to_customizer` nous allons ajouter notre propre section et nos propres champs qui permettent d'enregister nos propres règlages dans la base de données.


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

  /* ici  j'ajoute un control (autrement dit un champ input, textarea, select etc.) qui permettra à enregistrer notre setting */

  $wp_customize->add_control(
    'my_child_theme_custom_setting',
    array(
      'type'        => 'textarea', /* différents types sont disponible */
      'section'     => 'my_child_theme_custom_section', // Required, core or custom.
      'label'       => 'Mon option',
      'description' => 'Est sa description.',
    )
  );
}
```


`sanitize_callback` :

- `wp_kses_post` - filtre html
- `wp_filter_nohtml_kses` - filtre html et enlève tous les tags HTML
- `esc_url_raw` - filtre un url


## Comment "Consommer" l'option dans le template ?

```php
<?php echo get_theme_mod( 'my_child_theme_custom_setting' ); ?>
```

## Exemple 1 

```php
/* functions.php */
add_action(
		'customize_register', 'gridbox_child_add_stuff_to_customizer' );

function gridbox_child_add_stuff_to_customizer( $wp_customize ) {
  $wp_customize->add_section(
    'gridbox_child_custom_section',
    array(
      'title'       => 'Réglages Brioche et Canelle',
      'description' => 'Les options ajoutés via le thème gridbox-child',
    )
  );

		$wp_customize->add_setting(
			'gridbox_child_info_sponsor',
			array(
				'default'           => '',
				'sanitize_callback' => 'wp_kses_post',
			)
		);

		$wp_customize->add_control(
			'gridbox_child_info_sponsor',
			array(
				'type'        => 'textarea',
				'section'     => 'gridbox_child_custom_section',
				'label'       => 'Info sponsor',
				'description' => 'Texte affiché en haut de toutes les pages.',
			)
		);

		$wp_customize->selective_refresh->add_partial(
			'gridbox_child_info_sponsor',
			array(
				'selector' => '.sponsor-info',
			)
		);
}
```

```php
/* header.php */
<div class="sponsor-info">
  <?php echo get_theme_mod( 'gridbox_child_info_sponsor' ); ?>
</div>
```

## Exemple 2 (plus sécurisé)

```php
function gridbox_child_add_stuff_to_customizer( $wp_customize ) {
  $wp_customize->add_section(
    'gridbox_child_custom_section',
    array(
      'title'       => 'Réglages Brioche et Canelle',
      'description' => 'Les options ajoutés via le thème gridbox-child',
    )
  );

  $wp_customize->add_setting(
    'gridbox_child_info_sponsor_text',
    array(
      'default'           => '',
      'sanitize_callback' => 'wp_filter_nohtml_kses',
    )
  );

  $wp_customize->add_control(
    'gridbox_child_info_sponsor_text',
    array(
      'type'        => 'text',
      'section'     => 'gridbox_child_custom_section',
      'label'       => 'Info sponsor (text)',
      'description' => 'Texte affiché en haut de toutes les pages.',
    )
  );

  $wp_customize->add_setting(
    'gridbox_child_info_sponsor_link',
    array(
      'default'           => '',
      'sanitize_callback' => 'esc_url_raw',
    )
  );

  $wp_customize->add_control(
    'gridbox_child_info_sponsor_link',
    array(
      'type'        => 'text',
      'section'     => 'gridbox_child_custom_section',
      'label'       => 'Info sponsor (link)',
      'description' => 'Texte affiché en haut de toutes les pages.',
    )
  );
  
  $wp_customize->selective_refresh->add_partial(
    'gridbox_child_info_sponsor_text',
    array(
      'selector' => '.sponsor-info a',
    )
  );
}
```

et ensuite dans `header.php`

```php
/* header.php */
<div class="sponsor-info">
  <a href="<?php echo esc_url( get_theme_mod('gridbox_child_info_sponsor_link') ); ?>">
    <?php echo esc_html( get_theme_mod('gridbox_child_info_sponsor_text') ); ?>
  </a>
</div>
```

Pour renforcer la sécurité nous utilisons ici

- [`esc_html` - échappe les balises HTML](https://developer.wordpress.org/reference/functions/esc_html/)
- [`esc_url` - nettoie les urls](https://developer.wordpress.org/reference/functions/esc_url/)
- [`esc_attr` - échappe les `<`, `>`, `&`, `”`, `‘` dans les attributs](https://developer.wordpress.org/reference/functions/esc_attr/)