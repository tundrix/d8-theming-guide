
## Classy

`<div class="do-not-add-classes-in-drupal-core"></div>`

At DrupalCon Austin (2014) the need for a new core *base* theme came up. This need was part of what has been referred to as the **Consensus Banana**.

### Consensus Banana

> Where did the **banana** come from?
> 2 years before DrupalCon Austin, at BadCamp, John Albin ([JohnAlbin](https://www.drupal.org/u/johnalbin)) was holding a plastic sword from the pirate fest the day before. It was known as the sword of consensus. Morten ([mortendk](https://www.drupal.org/u/mortendk)) had a banana during the conference that he was using to point to people and ask “so can we agree on X?”. That is how it became the banana of consensus. It was basically a pointing stick.
> *Scott Reeves*

#### The meta issue

Here's a brief overview of [the meta issue](https://www.drupal.org/node/2289511):

> *Create a new core theme (code name "classy") that contains a copy of the all current core template files; this is for the "sensible 2/3" camp. And then modify all of the core/modules template files to contain minimal classes (only those needed for functionality); this would be for the "clean 1/3" camp. To ensure that Seven and Bartik continue to function properly, they should use "classy" as their base theme.*

#### Technical changes

Technically it comes down to this: the classes from core have been moved into the classy base theme. This was done in two phases. During the first phase the classes have been moved out of preprocess functions and moved into core template files. In the second phase the core template files with classes have been moved into Classy meaning all of the classes have been removed from core templates. You could now say that all the template files in core are now 'classless' (=no more `class="whatever"` in core).

Themers no longer require a base theme like [mothership](https://www.drupal.org/project/mothership) to *keelhaul the div*! A survey showed that not all themers want the same markup, and that they don't need all the wrapper <divs>. Thanks to Classy, no one has to waste any more time undoing core. The group of themers that wants sensible default classes can use classy as a base theme when developing their custom themes (more information on that later). The second group, that wants full control of all the markup and the classes, can start from scratch, without having to override anything, unlike the Drupal 7 experience.

### Classy, a new base theme

At DrupalCon Amsterdam, the **classy.info.yml** got commited into Drupal 8 core by Dries. The change record can be found [here](https://www.drupal.org/node/2337467).
This means Classy is the new `base theme` in Drupal core where *Bartik* and *Seven* are both extending from.

[Add classy.info.yml to core, set Classy as base theme for Bartik and Seven](https://www.drupal.org/node/2329501)

### Backwards compatibility

Classy can be relied on to maintain backwards compatibility throughout the Drupal 8 cycle.

***

**Read more**

* Modules Unraveled, episode 119: [The Classy Base Theme for Drupal 8 with Scott Reeves and David Hernandez](https://www.youtube.com/watch?v=uIutb2-Vc50).
* The official change record: [Added a new base theme to core called Classy](https://www.drupal.org/node/2337467)
