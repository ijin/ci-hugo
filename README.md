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

Add deploy key in [settings](https://github.com/ijin/serverlessdays-tokyo/settings/keys)

Title: `CircleCI-write`
Key: public ssh key
[x] Allow write access

### CircleCI

1. Add deploy key in `Project Settings`->`SSH Permissions`

Hostname: `github.com`
Key: private ssh key

2. ADD ssh fingerprint

Add Environment Variable

Name: `SSH_FINGERPRINT`
Value: *you ssh fingerprint*

## GitHub pages

```
git checkout --orphan gh-pages
git rm -rf .
git commit --allow-empty -m ':rocket:'
git push origin HEAD
```

## Configure CircleCI

set fingerprints to `add_ssh_keys` step in `.circleci/config.yml`

## Deploy

Just push/merge to git master branch, CircleCI will take care of the rest
