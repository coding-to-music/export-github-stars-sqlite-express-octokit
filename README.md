# export-github-stars-sqlite-express-octokit

# 🚀 A Node.js webapp to scrape the stars of specified GitHub users 🚀

https://github.com/coding-to-music/export-github-stars-sqlite-express-octokit

From / By https://github.com/umaar/export-github-stars

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/export-github-stars-sqlite-express-octokit.git
git push -u origin main
```

### GitHub Star Export

[![Actions Status](https://github.com/umaar/export-github-stars/workflows/Node%20CI/badge.svg)](https://github.com/umaar/export-github-stars/actions)

Export _all_ your GitHub stars.

![preview.png](preview.png)

This webapp queries the GitHub API to query for the stars of a GitHub user, and stores them in an SQLite database. 10,000 stars will occupy ~6mb worth of data.

This repo uses persistent queues, and supports resumable downloading of stars. You can fetch stars of many users.

![preview-jobs.png](preview-jobs.png)

#### To run

1. Get a GitHub token from https://github.com/settings/tokens

2. Create a `.env` file:

```
# Contents of .env

GITHUB_TOKEN=your token here

# Any name for your new database
DATABASE_NAME=output
```

3. Run these commands:

```sh
npm i
make migrate-db-dev
make start
```

### TODO:

- Send emails using an email service about database size changes
- Automatically update user stars every ~ few hours
- Insert stars/repos using transactions in bulk
- Implement ajax for pagination
- Cache users and their star counts
- Use http://nvd3.org/ to visualise a users stars over time
- For many stars, should I use something like this https://github.com/tbranyen/hyperlist
- Configure pooling correctly: https://github.com/tgriesser/knex/issues/2820#issuecomment-481710112 e.g.

```
"pool": {
  "min": 2,
  "max": 6,
  "createTimeoutMillis": 3000,
  "acquireTimeoutMillis": 30000,
  "idleTimeoutMillis": 30000,
  "reapIntervalMillis": 1000,
  "createRetryIntervalMillis": 100,
  "propagateCreateError": false // <- default is true, set to false
},
```
