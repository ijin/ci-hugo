# CircleCI Hugo to GitHub pages

## Site Generator

The site is built on top of [Hugo](https://gohugo.io).

[Installation](https://gohugo.io/getting-started/installing/)

## Localdev

```
hugo serve -D -s src/site
```

## Deploy Key

### local
Create a deploy key

```
ssh-keygen -m pem -t rsa
```

### GitHub

Add deploy key in repository

Title: `CircleCI-write`
Key: public ssh key
[x] Allow write access

### CircleCI

1. Add deploy key in `Project Settings`->`SSH Permissions`

Hostname: `github.com`
Key: private ssh key

2. ADD ssh fingerprint

ADD ssh finger prints with `add_ssh_keys` to `.circleci/config.yml`

## GitHub pages

```
git checkout --orphan gh-pages
git rm -rf .
mkdir .circleci
cat <<EOF > .circleci/config.yml
version: 2
jobs:
  build:
    branches:
      only: master
EOF
git add .circleci
git commit -m ':rocket:'
git push origin gh-pages
git checkout master
```

## Configure CircleCI

Set fingerprints to `add_ssh_keys` step in `.circleci/config.yml`

## Set custom domain

Set custom domain in repository settings

## Deploy

Just push/merge to git master branch, CircleCI will take care of the rest
