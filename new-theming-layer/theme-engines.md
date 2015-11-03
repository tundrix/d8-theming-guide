# Theme engines

Inside `core/themes` there is a fifth folder (besides `bartik`, `seven`, `stark` and `classy`), called `engines`. This folder contains the theme engines. The default template engine In Drupal 8 is **Twig**. The default template engine from Drupal 7 however, PHPTemplate, does still live in there. It's not recommended to continue using the PHPTemplate engine. Bear in mind that Twig has a lot more to offer and is much more secure than PHPTemplate.

## What is a theme engine?

A theme engine (also called template engine, template processor or template parser) is a software component that **combines data with templates** from themes and shows the result - the final HTML - to the user.

![Template Engine](https://raw.githubusercontent.com/sqndr/d8-theming-guide/master/img/template-engine.png)
