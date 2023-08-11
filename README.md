# gh-api-reproducer

Fetching commits via gh api

## Test chars

- 🇮🇪

  - : Flag emoji

- �

  - : Unicode replacement character

## Steps to reproduce

Use the `gh` cli to fetch commits from this repo:

```bash
gh api repos/bsmth/gh-api-reproducer/commits/81d0f58fbadb176ccfd292240b87e474f4b5c848
# invalid UTF-8 string
```

## Expected result

A full JSON response is returned:

```json
{
  // ...
  "files": [
    {
      // ...
      "patch": "@@ -1,3 +1,5 @@\n []: # Path: README.md\n # gh-api-reproducer\n \n+Fetching commits via gh api\n+\n ## Test chars\n \n - �\n  - : Unicode replacement character\n ..."
  // ...
}
```

## Actual result

JSON output is truncated / broken at the `patch` key at the point where the character is encountered:

```json
{
  // ...
  "patch": "@@ -1,3 +1,5 @@\n []: # Path: README.md\n # gh-api-reproducer\n \n+Fetching commits via gh api\n+\n ## Test chars\n \n -
```

## Example passing command

If the patch is parsed correctly, we can get the patch contents:

```bash
gh api repos/bsmth/gh-api-reproducer/commits/1b33e078374c5d3e596c16ea4a02c735191b21ec --jq '.files[].patch'
```
