# Libraries

Libraries are the most imported part for Drupal 8 themes. They are used to add any kind of assets (css or javascript) to the page.

## Global styling

Stylesheets that should be included on all pages are called globing styling. It's considered a good practice to use `{theme}/globing-styling` as a key for this sort of stylesheets.

## Global scripts

Scripts that should be included on all pages are called globing scripts. It's considered a good practice to use `{theme}/globing-scrips` as a key for this sort of javascript.

> **NOTE:** Don't just include all your css or javascript files on every page!

## Adding a javascript library

Here is an example of how to add a custom javascript file to theme.

Start by creating a `*.libraries.yml` file, e.g. `awesome.libraries.yml` (`{theme-or-module-name}`.libraries.yml) and save it into the root of the theme.

    base:
      version: 1.x
      js:
        js/awesome.js: {}
      dependencies:
        - core/drupal
        - core/jquery
        - core/jquery.once

> We need `core/drupal` in order to take advantage of the `Drupal.behaviors`. To include the Drupal core version of jQuery, we add `core/jquery`. The final dependency is `core/jquery.once`, a jQuery plugin allowing to only apply a function once to an element.

Open up the `*.info.yml` file of the theme and add the following lines to include the *library* into the theme.

    libraries:
      - awesome/base

This includes the custom javascript and also makes sure that all dependencies are loaded. For example: Drupal will make sure that jQuery is loaded before importing `awesome.js`.
