## stable

`base theme: stable` or when you don't define a base theme.

*Stable* was introduced in Drupal 8 as a backwards compatibility layer for Drupal 8's core markup, CSS and JS. When no `base theme` is provided by a theme, stable will automatically be used.

> This change allows core markup, CSS and JS to further evolve throughout Drupal 8, while still allowing themes to have a stable base for the clean, minimal markup provided by Drupal 8 core. This is especially useful for front-end developers who would prefer to add in their own classes to markup where needed, rather than remove Drupal's default classes. Front-end framework implementations like Bootstrap or Foundation might find this particularly useful.

To disable backwards compatibility, a theme can still directly extend core by setting the base theme to `false`:

    base theme: false

***

* The official change record: [Stable base theme added as default for backwards compatibility](https://www.drupal.org/node/2580687)
