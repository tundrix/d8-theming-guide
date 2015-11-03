# Drupal core themes

The four Drupal 8 **core** themes live inside the `core/themes` folder. As part of the Drupal 8 Mobile Initiative all of Drupal core's themes have been converted to a  responsive design.

> **NOTE:** Stark had a stylesheet inside the theme to make sure the regions were responsive. However, this stylesheet got removed. **Read more on this in the Stark section.**

- **bartik**: *A flexible, recolorable theme with many regions and a responsive, mobile-first layout.*
- **seven**: *The default administration theme for Drupal 8 was designed with clean lines, simple blocks, and sans-serif font to emphasize the tools and tasks at hand.*
- **stark**: *An intentionally plain theme with almost no styling to demonstrate default Drupal’s HTML and CSS.*

You might remember these three themes from Drupal 7. But wait, there's more ...

- **classy**: [[meta] Results of Drupalcon Austin's Consensus Banana](https://www.drupal.org/node/2289511): At DrupalCon Austin (2014) the need for a new core theme came up. Classy is a base theme that Seven and Bartik will extend from.
- **stable**: The Stable theme will function as a backwards compatibility layer for Drupal 8's core markup, CSS and JS. A theme will use Stable as the base theme if no base theme is set in its .info.yml file.

----

Here's an overview of the Drupal 8 core themes and how they relate to each other.

![An overview of the core themes](../img/theme-overview.png)
