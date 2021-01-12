# Twig

These coding standards are based upon the [official Twig coding standards document](https://twig.symfony.com/doc/3.x/coding_standards.html).

Put one (and only one) space after the start of a delimiter and before the end of a delimiter:

```twig
{{ foo }}
{# comment #}
{% if foo %}
    ...snip...
{% endif %}
```

Put one (and only one) space before and after the following operators: comparison operators, math operators, logic operators, and the ternary operator:

```twig
{{ 1 + 2 }}
{{ foo ~ bar }}
{{ true ? true : false }}
```

Put one (and only one) space after the `:` sign in hashes and `,` in arrays and hashes:

```twig
{{ [1, 2, 3] }}
{{ {'foo': 'bar'} }}
```

Do not put any spaces before and after the following operators: `| . .. []`:

```twig
{{ foo|upper|lower }}
{{ user.name }}
{{ user[name] }}
{% for i in 1..12 %}
    ...snip...
{% endfor %}
```

Indent your code inside tags (use the same indentation as the one used for the target language of the rendered template):

```twig
{% block foo %}
    {% if true %}
        ...snip...
    {% endif %}
{% endblock %}
```

Use camelcase variable names:

```twig
{% set foo = "foo" %}
{% set fooBar = "foo" %}
```