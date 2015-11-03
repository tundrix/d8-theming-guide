### jQuery

Drupal 8 doesn't load any additional scripts by default. This means that [jQuery is not included](https://www.drupal.org/node/1541860) on every page any more. This is mostly due to performance reasons: you don't need jQuery on every page, so Drupal should only load it when needed. In order to use jQuery, you have to declare jQuery (or any other core library) as a dependency for your script. 

> Since Drupal 8 does not support IE8 - and below - and because Javacript has evolved, [you might not need jQuery](http://youmightnotneedjquery.com/). If however you do want to use jQuery, make sure to look up the [best practices](http://lab.abhinayrathore.com/jquery-standards/) for using jQuery.

#### jQuery and Drupal

Drupal uses jQuery in a no-conflict mode. In jQuery, `$` is an alias for `jQuery`. Other javascript libraries often use `$` as a function or variable name. When using jQuery in a no-conflict mode, this `$` variable is released so other libraries can use this `$` variable.
