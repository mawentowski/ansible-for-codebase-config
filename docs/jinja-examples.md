# Jinja guide

## Referencing arrays of objects

For an object defined is `repo.yaml`, such as:

```yaml
todo:
  - text: Implement new feature
    state: open
```

Whose schema looks like:

```yaml
todo:
  type: array
  items:
    type: object
    properties:
      text:
        type: string
      state:
        type: string
        enum:
          - open
          - in-progress
          - done
```

Generate a list of a specific property within each object:

```shell
{% for todo in repo.todo %}
- {{ todo.text }}
{% endfor %}
```

## Generate list of array items

For an array defined is `repo.yaml`, such as:

```yaml
gitignore:
  - .github
  - .husky
  - .dockerignore
  - .editorconfig
  - CODEOWNERS
  - commitlint.config.js
  - LICENSE
  - README.md
  - SECURITY.md
```

Whose schema looks like:

```yaml
gitignore:
  type: array
```

Generate a list of array items:

```shell
{% if repo.gitignore is defined %}
{% for file in repo.gitignore %}
{{ file }}
{% endfor %}
{% endif %}
```

## Generate a list for object properties whose values are arrays of strings

For an object defined is `repo.yaml`, such as:

```yaml
codeowners:
  /:
    - mawentowski
    - mawentowski
  /docs:
    - mawentowski
```

Whose schema looks like:

```yaml
codeowners:
  type: object
  patternProperties:
    "^/.*$":
      type: array
      items:
        type: string
```

Generate a list for each property containing the property followed by array items:

```yaml
{% for path, owners in repo.codeowners.items() %}
{{ path }}
{% for owner in owners %}
{{ owner }}
{% endfor %}
{% endfor %}
```

Note: The usage of `patternProperties` signifies that the properties are determined by regular expression patterns.
