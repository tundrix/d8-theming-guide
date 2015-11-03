## The history of libraries, part 1

During the early development of Drupal 8, assets such as javascript and stylesheets had their own, different way of getting imported into themes. Importing a custom javascript file was done using the `scripts` property inside the `.info.yml`-file of the theme. To import stylesheets, the `stylesheets` property was used. This was more or less the way it was done in Drupal 7. Here is an example from a Drupal 7 `theme.info` file.

    ...

    # Adding stylesheets
    stylesheets[all][] = css/styles.css
    stylesheets[print][] = css/print.css

    # Adding javascript files
    scripts[] = js/script.js

    ...

An alternative path was chosen. Javascript maintainer **_nod** created an issue on [using AMD for JS architecture](https://www.drupal.org/node/1542344). The patch for the issue became so big that a separate issue was created. This issue handled the splitting up of the dependencies. This patch, [Explicitly declare all JS dependencies, don't use drupal_add_js](https://www.drupal.org/node/1737148), where all javascript files are declared as libraries and added the relevant dependencies to the scripts, got committed about two weeks after the creation. The original issue [**AMD architecture**] however was posponed to a later Drupal release (Drupal 9.x).

## {}.libraries.yml

During the early stages of Drupal 8, this was done using `hook_library_info`. Since this was one of the last remaining hooks in Drupal 8, it got [replaced by a `*.libraries.yml` file](https://www.drupal.org/node/2201089)). This means modules, themes and profiles can define their own `*.libraries.yml` file. The file should be in the root directory of the theme (or module).

    # example.libraries.yml

    base:
      version: 1.x
      js:
        js/scripts.js: {}
      css:
        component:
          css/components/component.css: {}
      dependencies:
        - core/drupal
        - core/jquery

Inside the `.info.yml` file from a module or theme, the library can be included using the `libraries` property.

    # example.info.yml

    libraries:
      - example/base

The *example* theme now has a global dependency on the `base` library (from the *example* theme/module); `example/base`. Therefor it's included on **every page** (where this theme is loaded). The `base` library itself contains a single javascript file (`scripts.js`), a css file (categoried as a component) and has dependencies on the `drupal` and `jquery` library from core (read more on this in the **Javascript** chapter).

## The history of libraries, part 2

Due to this change, the `scripts` tag from the `.info.yml`, was removed and replaced with the `libraries` property. This means scripts can only be included using the `libraries` property and a `libraries.yml` file. Stylesheets however (in themes) could still included using the old `stylesheets` property:

**_nod**:

> remove scripts[] from info files and replace it with library[] …

> stylesheets[] can be kept as is, it's totally fair to add a single css file without dependencies. It's highly unlikely for scripts, they will need to depend on jquery, drupal.js 99% of the time.

It became clear this new way of adding assets had some major advantages. Wim Leers created a new issue stating [Themes should use libraries, not individual stylesheets](https://www.drupal.org/node/2377397). Due to the advantages pointed out in this issue, the `stylesheets` property from the `.info` file got removed. Thanks to this, there is now a unified way for adding assets libraries.
