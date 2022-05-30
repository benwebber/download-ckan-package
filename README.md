# get-ckan-package

A [GitHub action](https://docs.github.com/en/actions) that downloads resources from a [CKAN](https://ckan.org/) package.

This action fetches:

* the package metadata (as `${package_id}.json`)
* all resources in the package, or a subset of resources specified by `resource_ids`

This action is particularly useful for [Git scraping](https://simonwillison.net/series/git-scraping/) data from a CKAN portal.

## Usage

```yaml
steps:
  - uses: actions/checkout@v3

  - uses: benwebber/get-ckan-package@v1
    with:
      url: https://ckan.example.org/
      package_id: 1d2bf6b7-3961-444f-8f9b-2f227531f5de
      output_dir: data/
      resource_ids: '["d600fcdd-b148-4a65-84c5-13380348913f","b8b0d9d0-ca2c-430a-9726-d8884f770c2e"]'

   - run: |-
      git config user.name "github-actions[bot]"
      git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
      git add data/
      git commit -m 'Fetched new data' || exit 0
      git push
```

## Inputs

### `url`

**Required.**

The CKAN server URL.
Do not include the API path (`/api`).

### `package_id`

**Required.**
The CKAN package ID.

### `output_dir`

Optional.
Specify an output directory for the package metadata and resources.

### `resource_ids`

Optional.
Only download the resources with these IDs.
If not specified, download all resources in the package.
This input is a JSON array.
