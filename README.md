# Aarhus kommune – a Kimai plugin

## Installation

Download [a release](https://github.com/itk-kimai/kimai-plugin-AarhusKommuneBundle/releases) and move it to `var/plugins/`.

```shell
bin/console kimai:reload --no-interaction
```

Edit your [`local.yaml`](https://www.kimai.org/documentation/local-yaml.html#localyaml):

``` yaml
# config/packages/local.yaml
aarhus_kommune:
    primary_project: 87
    primary_activity: 42
```

See [Install and update Kimai plugins](https://www.kimai.org/documentation/plugin-management.html) for details.

Go to `/da/aarhus-kommune/timesheet/create` and enjoy.

## Features

### App template overrides

To override the app template `templates/partials/ticktack.html.twig`, say, create a template in
`Resources/views/app/partials/ticktack.html.twig`:

``` twig
{# Resources/views/app/partials/ticktack.html.twig #}

{# Use `@App` to refer to the original template #}
{{ include('@App/partials/ticktack.html.twig') }}
```

The path after `Resources/views/app/` _must_ match the path after `templates/partials/` exactly.

Another example:

``` twig
{# Resources/views/app/base.html.twig #}
{% extends '@App/base.html.twig' %}

{% block page_content_after %}
    <div class="float-help">
        <a href="https://aarhuskommune.dk/tid" target="_blank" accesskey="h" title="{{ 'help'|trans }}">
            <i class="fas fa-question"></i>
        </a>
    </div>
    <div class="mb-4"></div>
{% endblock %}
```

## Development

``` shell
git clone --branch develop https://github.com/itk-kimai/kimai-plugin-AarhusKommuneBundle var/plugins/AarhusKommuneBundle
bin/console kimai:reload --no-interaction
```

### Coding standards

``` shell
docker run --rm --volume ${PWD}:/app --workdir /app itkdev/php8.3-fpm composer install
docker run --rm --volume ${PWD}:/app --workdir /app itkdev/php8.3-fpm composer coding-standards-apply
docker run --rm --volume ${PWD}:/app --workdir /app itkdev/php8.3-fpm composer coding-standards-check
```

``` shell
docker run --rm --volume "$(pwd):/md" peterdavehello/markdownlint markdownlint --ignore LICENSE.md --ignore vendor/ '**/*.md' --fix
docker run --rm --volume "$(pwd):/md" peterdavehello/markdownlint markdownlint --ignore LICENSE.md --ignore vendor/ '**/*.md'
```

``` shell
docker run --rm --volume ${PWD}:/app --workdir /app itkdev/php8.3-fpm composer install
docker run --rm --volume ${PWD}:/app --workdir /app itkdev/php8.3-fpm composer code-analysis
```

*Note*: During development you should remove the `vendor/` folder to not confuse Kimai's autoloading.
