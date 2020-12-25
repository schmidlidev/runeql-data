# runeql-data

![Upload Data](https://github.com/schmidlidev/runeql-data/workflows/Upload%20Data/badge.svg)

This repository is the staging area for static data served by RuneQL. (Items, Monsters, etc)
This repository does *not* contain the dynamic data served by RuneQL (Live grand exchange prices, hiscores, etc).

## Source of data

All of the data in this repository is originally sourced from the incredible [osrsbox project](https://github.com/osrsbox/osrsbox-db). The content and structure of osrsbox data is then transformed to better serve a graphql API. The tooling for this process is maintained in [runeql-tools](https://github.com/schmidlidev/runeql-tools).

### How does the data arrive here?
1. Updates to the [osrsbox-db](https://github.com/osrsbox/osrsbox-db) `master` branch are automatically propagated to [a fork](https://github.com/schmidlidev/osrsbox-db) using https://github.com/wei/pull.
2. The fork houses a [GitHub actions workflow](https://github.com/schmidlidev/osrsbox-db/blob/master/.github/workflows/runeql-data%20update.yml) that uses [runeql-tools](https://github.com/schmidlidev/runeql-tools) actions to trigger the data transformation, commit the new data to the `update` branch in this repository, and open a pull request for it into `main`.
3. Accepting the pull request serves as a push-button deployment.

### Where does the data go from here?
Commits to `main` trigger a [workflow](https://github.com/schmidlidev/runeql-data/blob/main/.github/workflows/Upload.yml) that upserts the data to the live RuneQL MongoDB database cluster.
