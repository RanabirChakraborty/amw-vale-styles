# amw-vale-styles

Shared [Vale](https://vale.sh/) vocabularies for the [ansible-middleware](https://github.com/ansible-middleware) collections.

Each collection has its own directory containing an `accept.txt` of terms Vale should not flag as spelling errors.

## Structure

```
<collection-name>/
└── accept.txt
```

| Directory | Collection |
|-----------|-----------|
| `WildFly/` | [wildfly](https://github.com/ansible-middleware/wildfly) |

## Adding a new collection

1. Create a directory named after the collection.
2. Add `accept.txt` with one Vale regex pattern per line.
3. In the collection's `.github/workflows/lint-prose.yml`, add a download step before Vale runs (see below).
4. In the collection's `.vale.ini`, add the vocab name to the `Vocab` line.

### CI step to add in `lint-prose.yml`

```yaml
- name: Download shared vocabulary
  run: |
    mkdir -p .github/styles/config/vocabularies/<CollectionName>
    curl -sL https://raw.githubusercontent.com/ansible-middleware/amw-vale-styles/main/<CollectionName>/accept.txt \
      -o .github/styles/config/vocabularies/<CollectionName>/accept.txt
```

### `.vale.ini` change

```ini
Vocab = Base, <CollectionName>
```

## Adding words

Edit the relevant `<collection-name>/accept.txt` and open a PR. Entries are Vale regex patterns — one per line.

## Local development

Run the same curl command from the CI step above to download the vocabulary before running `vale` locally.
