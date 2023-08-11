# gh-api-reproducer

Fetching commits via gh api

## Test chars

- TODO
  - : Unicode replacement character

## Steps to reproduce

Use the `gh` cli to fetch commits from this repo:

```bash
gh api repos/bsmth/gh-api-reproducer/commits/{commit-sha} > output.json
tail output.json
```

## Expected result

```json
{
  // ...
  "patch": "@@ -1,3 +1,5 @@\n []: # Path: README.md\n # gh-api-reproducer\n \n+Fetching commits via gh api\n+\n ## Test chars\n \n - TODO\n \n"
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
