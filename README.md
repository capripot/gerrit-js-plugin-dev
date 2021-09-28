# Gerrit js plugin dev

Starter pack for Gerrit javascript plugin development.

## Install

- Code > Download ZIP
- Unarchive zip file
- Install [Docker](https://www.docker.com/get-started)
- Install [Puma-dev](https://github.com/puma/puma-dev)
  - `brew install puma/puma/puma-dev`
  - `puma-dev -install`
  - `sudo puma-dev -setup`
- `echo 3200 > ~/.puma-dev/gerrit`

## Start

- `docker-compose up`
- Go to https://gerrit.test

## Setup

- Go to top right > Settings
- Add your Git email (`git config --get user.email`)
- Add your SSH public key (`cat ~/.ssh/id_rsa.pub`)
- Clone All-projects `git clone ssh://gerrit.test:29418/All-Projects`
- `cd All-Projects`
- Install Change-Id hook
  - `gitdir=$(git rev-parse --git-dir); scp -p -P 29418 gerrit.test:hooks/commit-msg ${gitdir}/hooks/`
- Create a `main` branch
  - `git checkout -b main`
  - `git push origin`
- Create a change
  - `git checkout -b change1`
  - `git push origin HEAD:refs/for/main`
- Change URL is returned by Gerrit

## Develop your plugin

- `git init`
- Update the Gerrit version you want to develop against in `docker-compose.yml`
  (3.2.12 is the current default)
- Rename template `mv plugins/plugin-v1.0.0.template.js plugins/mysuperplugin-v1.0.0.js`
  `mysuperplugin` is the name of the plugin (`[a-z]+`) and `v1.0.0` is the version of the plugin.

Gerrit watches the plugins folder for changes and will reload the plugin.
Then, reload your page to load the new version.

## Links

- Docker images: https://hub.docker.com/r/gerritcodereview/gerrit/tags
- Docker image repo: https://github.com/GerritCodeReview/docker-gerrit
- Doc: https://gerrit.test/Documentation/ or https://gerrit-review.googlesource.com/Documentation/
- JS API doc: https://gerrit.test/Documentation/js-api.html
