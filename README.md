# GitHub to Guru
Create cards in a Guru collection based on content in a GitHub repo

## Outputs

### `created`

Number of Guru cards created

## Example usage

1. Add a Secret named `GURU_USER_TOKEN` containing a [User Token for Guru](https://help.getguru.com/articles/XipkRKLi/Guru-API-Overview)

2. Add a Secret named `GURU_USER_EMAIL` containing the email address for which you [created the User Token](https://app.getguru.com/settings/api-access)

3. Add a workflow file which responds to file changes, customizing GURU_COLLECTION_ID to the `id` of a collection found at https://api.getguru.com/api/v1/collections. Also update `FILE_LIST` in the env: it should be a JSON object in which each key is a markdown file in your repo, and each value is the title for the Guru card it creates.

```yaml
name: Create guru cards

on: [push]

jobs:
  guru:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: peckjon/github-to-guru@master
      env:
        GURU_USER_EMAIL:  '${{ secrets.GURU_USER_EMAIL }}'
        GURU_USER_TOKEN:  '${{ secrets.GURU_USER_TOKEN }}'
        GURU_COLLECTION_ID: '********-****-****-****-************'
        FILE_LIST: |
          {
            "something.md": "Title for the Something Card",
            "some_other_thing.md": "Title for the Other Thing Card"
          }
```
