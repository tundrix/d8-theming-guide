### Drupal behaviors (`Drupal.behaviors`)

Drupal behaviors (`Drupal.behaviors`) are still part of javascript in core. These behaviors will be executed on every request, including AJAX requests.

> Don't forget to add a dependency to `core/drupal` in order to use Behaviors.

Below is an example of a Drupal Javascript Behavior.

    (function ($) {
      'use strict';
      Drupal.behaviors.awesome = {
        attach: function(context, settings) {
          $('main', context).once('awesome').append('<p>Hello world</p>');
        }
      };
    }(jQuery));

Let's have a quick look at what this does.

- **namespace**:
A Drupal behavior has to have a unique namespace. In this example, the namespace is `awesome` (`Drupal.behaviors.awesome`).

- **attach**:
Contains the actual function that should be executed.

- **context**:
The `context` variable is the part of the page for which this applies. On a page load, this will be the entire document. On a AJAX request however, the `context` variable will only contain all the newly loaded elements.

- **settings**:
The `settings` variable is used to pass information from the PHP code to the javascript (`core/drupalSettings`).

- **once**:
Using the `.once('awesome')` will make sure the code only runs once. Otherwise, the code will be executed on every AJAX request. It adds a `processed`- class to the `main` tag (`<main role="main" class="awesome-processed">`) in order to accomplish this (`core/jquery.once`).

      (function ($) {
        'use strict';

        Drupal.behaviors.awesome = {
          attach: function(context, settings) {
          },
          detach: function (context, settings, trigger) {
          }
        };

      }(jQuery));

- **detach**:
Alongside `attach` lives `detach`, which can be used to detach registered behaviors from a page element. Besides from a `context` and `settings`, it also expects a `trigger`. The `trigger` is a string containing the causing of the behavior to be detached. Possible causings are:

  - *unload*: (default) The context element is being removed from the DOM.
  - *move*: The element is about to be moved within the DOM (for example,
  during a tabledrag row swap). After the move is completed,
  Drupal.attachBehaviors() is called, so that the behavior can undo
  whatever it did in response to the move. Many behaviors won't need to
  do anything simply in response to the element being moved, but because
  IFRAME elements reload their "src" when being moved within the DOM,
  behaviors bound to IFRAME elements (like WYSIWYG editors) may need to
  take some action.
  - *serialize*: When an Ajax form is submitted, this is called with the
  form as the context. This provides every behavior within the form an
  opportunity to ensure that the field elements have correct content
  in them before the form is serialized. The canonical use-case is so
  that WYSIWYG editors can update the hidden textarea to which they are
  bound.
