## Attach libraries directly from a template file

As mentioned, the libraries inside the `*.info.yml` file are include globally, on every page. To conditionally add a library, a `preprocess` function (`#attached`), just like in Drupal 7, had to be used. In order to improve the front-end developer experience, a simple Twig function has been added to easify this. ``{{ attach_library('theme/library') }}`` makes it possible to add libraries directy from template files. A huge win.

> The only template files that doesn't support this is **html.html.twig**. More information can be found [here](https://www.drupal.org/node/2398331#comment-9745117).
