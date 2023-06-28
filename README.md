# Github Import

Imports projects from Github repos since a given date.

> Note: This module is a proof of concept for how you can use the Boss-Net import API. We hope to roll the findings from this module into the Boss-Net website eventually, so consider this a work in progress.

## Prerequisites

To use this tool you must first set an environment variable `BOSS_TOKEN` with
your API key, as found at https://boss-net.github.io/account.

## Installation

You can install this globally by running:

```bash
npm install -g @boss-net/github-import
```

You can find usage instructions by running:

```bash
github-import --help
```

## Usage

To find out the available arguments, type the following command:

```bash
github-import --help
```

To import all repos modified in the last day (since the beginning of the day, yesterday) you can run the following command:

```bash
github-import --orgId=<orgId> --integrationId=<integrationId> --githubToken=<githubToken> --githubUrl=<baseUrl>
```

To import all repos for a specific GitHub organisation you can run the following command:

```bash
github-import --orgId=<orgId> --integrationId=<integrationId> --githubToken=<githubToken> --githubUrl=<baseUrl> --githubOrg=<githubOrgName>
```

If you wish to expand the number of days, you can specify with the `days` argument:

```bash
github-import --orgId=<orgId> --integrationId=<integrationId> --githubToken=<githubToken> --githubUrl=<baseUrl> --days=<number>
```

To import all repos modified since a specific dateTime (in the ISO 8601 format `YYYY-MM-DDThh:mm:ss.sssZ`) you can run the following command:

```bash
github-import --orgId=<orgId> --integrationId=<integrationId> --githubToken=<githubToken> --githubUrl=<baseUrl> --since=<dateTime>
```

We recommend setting up a cron job to run this script daily at most.

- You can retrieve your `orgId` from your org settings page on [Boss-Net](https://boss-net.github.io).
- The `integrationId` is available via the integration settings page.
- You can generate a token for access to the GitHub API from your [Personal access tokens](https://github.com/settings/tokens) page.
- The Github URL is only required for Github Server instances and is the base URL that your GitHub Server is available at.

## How this works

When you run `github-import`, it retrieves all repos that were modified since the date you specify (defaults to 1 day). It then calls the Boss-Net import API with those repos, which will attempt to import projects from the given repos. If any new target files are found in these repos, this will result in a new project being created.

Please note that this will trigger a retest of any projects that were already imported.
