## Twig basics

### Twig autoescape enabled

> To escape a string means to reduce ambiguous characters in a string.

[Twig autoescape enabled](https://www.drupal.org/node/2296163) by default. This means that every string printed from a Twig template (anything between `{{ }}`) gets *escaped*.

### Printing a variable

To print a simple variable in a template, use `{{ variable }}`, eg. `{{ foo }}`

A dot (`.`) can be used to access attributes of a variable:

    {{ foo.bar }}

>    Twig will automatically check for the following options:

    // Array key.
    $foo['bar'];
    // Object property.
    $foo->bar;
    // Object method.
    $foo->bar();
    // Object get method convention.
    $foo->getBar();
    // Object is method convention.
    $foo->isBar();
    // Object dynamic object property is set and get property.
    $foo->__isset('bar');
    $foo->__get('bar');

*PHP*

    $awesome_array = array(
      'a_key' => 'a_value',
      'another_key' => array(
        'foo' => 'bar',
      ),
    );

*Twig*

    {{ awesome_array.a_key }} # returns 'a_value'
    {{ awesome_array.another_key.foo }} # returns 'bar'

### Twig filters

It's possible to let the variable go through a filter before printing it. This can be done using `{{ variable|filter }}`.


#### Twig filters

Here are some example of filters from the Twig engine.

- `|length`, returns the number of items of a sequence or mapping, or the length of a string.
- `|lower`, converts a value to lowercase.
- `|upper`, converts a value to uppercase.
- …

A complete list of default Twig filters [can be found here](http://twig.sensiolabs.org/doc/filters/index.html).

#### Drupal filters

Drupal offers some additional filters.

##### Translation filters

- `t` will run the variable through the Drupal `t()` function, which will return a translated string. An example:
{% raw %}<a href="{{ url('<front>') }}" title="{{ 'Home'|t }}" rel="home" class="site-logo"></a>{% endraw %}

- `passthrough`
- `placeholder`

To safely escape all of the Twig variables detected in a `{% trans %}` tag, the variables are sent with an `@` prefix by default. To pass-through a variable (**!**) or use as a placeholder (**%**), the `passthrough` or `placeholder` filters are used.

- **passthrough** gets no sanitization or formatting and should only be used for text that has already been prepared for HTML display.
- **placeholder** gets escaped to HTML and formatted using [drupal_placeholder()](https://api.drupal.org/api/drupal/core%21includes%21bootstrap.inc/function/drupal_placeholder/8), which makes it display as <em>emphasized</em> text.

- `raw` will show the raw data (meaning without any escaping).

##### Replace twig's escape filter with our own.

- `drupal_escape` is a replacement function for Twig's escape filter. See [twig_drupal_escape_filter](https://api.drupal.org/api/drupal/core%21themes%21engines%21twig%21twig.engine/function/twig_drupal_escape_filter/8)

##### Implements safe joining.

- `safe_join` to safely joins several strings together. See [twig_drupal_join_filter](https://api.drupal.org/api/drupal/core%21themes%21engines%21twig%21twig.engine/function/twig_drupal_join_filter/8)

##### Array filters

- `without` creates a copy of the renderable array and removes child elements by key specified through filter's arguments. The copy can be printed without these elements. The original renderable array is still available and can be used to print child elements in their entirety in the twig template.

##### CSS class and ID filters.

- `clean_class` prepares a string for use as a valid HTML class name. [From Html::getClass](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Component%21Utility%21Html.php/function/Html%3A%3AgetClass/8)
- `clean_id` prepares a string for use as a valid HTML ID. [From Html::getId](https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Component%21Utility%21Html.php/function/Html%3A%3AgetId/8)

#### Translations

The Twig i18n extension allows marking parts of a template as translatable. Let's start of with an easy example:

  `{%trans %} Hello world {% endtrans %}`

It's possible to embed a variable in a translatable string, using the `{{ variable }}` syntax.

  `{%trans %} Hello {{ name }} {% endtrans %}`

To apply a filter to a variable, used in a translatable block you first need to assign the result to a variable.

    {% set name = name|capitalize %}

    {% trans %}
      Hello {{ name }}!
      {% endtrans %}

A translatable string can be pluralized. Implementing a `{% plural ... %}` switch makes this possible.

    {% trans %}
      Hello star.
    {% plural count %}
      Hello {{ count }} stars.
    {% endtrans %}

#### Comments

`{# Comments go inside these brackets. #}`

#### Functions

An `if` function.

    {% if site_slogan %}
      <div class="site-slogan">{{ site_slogan }}</div>
    {% endif %}

#### Loops

A `for` function. The output for this is `0, 1, 2, 3`.

> The `range` function returns a list containing an arithmetic progression of integers.

    {% for i in range(0, 3) %}
      {{ i }},
    {% endfor %}

Another example, from the `field--node--title.html.twig` template:

    {% for item in items %}
      {{ item.content }}
    {% endfor %}

Inside of a for loop block you can access some special variables.

| Variable       | Description                                                    |
|----------------|----------------------------------------------------------------|
| items.index     | The current iteration of the loop. (1 indexed)                |
| items.index0    | The current iteration of the loop. (0 indexed)                |
| items.revindex  | The number of iterations from the end of the loop (1 indexed) |
| items.revindex0 | The number of iterations from the end of the loop (0 indexed) |
| items.first     | `True` if first iteration                                       |
| items.last      | `True` if last iteration                                        |
| items.length    | The number of items in the sequence                           |
| items.parent    | The parent context                                            |

A replacement block can be rendered if no iteration took place (because the sequence was empty). This can be done by using `else`.

    <ul>
    {% for user in users %}
      <li>{{ user.username|e }}</li>
    {% else %}
      <li><em>no user found</em></li>
    {% endfor %}
    </ul>

#### Create a Twig variable

Sometimes it might be useful to define variables in a template file. `{% set foo="bar" %}` declares a variable `foo` and assigns the value `bar` to it. Later in the template, the variable can be printed out using `{{ foo }}`.

    example.twig.php
    ---

    {% set foo="bar" %}

    # Other code here

    Hi, here's my variable: {{ foo }}

The variable can be a single value, as mentioned in the example above, but it can also be an array:

    another_example.twig.php
    ---

    {%
      set foo_array = [
        'foo',
        'bar',
      ]
    %}
