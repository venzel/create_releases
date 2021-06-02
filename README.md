# README.md

#teste

## Pacotes necessários

```bash
$ yarn add @commitlint/cli @commitlint/config-conventional husky -D
```

```bash
$ yarn add semantic-release @semantic-release/changelog @semantic-release/git -D
```

## Configurações para o package.json

```JSON
{
    "name": "releases",
    "version": "0.1.0",
    "main": "index.js",
    "private": true,
    "license": "MIT",
    "repository": {
        "type": "git",
        "url": "git@github.com:venzel/releases.git"
    },
    "scripts": {
        "release": "semantic-release --no-ci"
    },
    "commitlint": {
        "extends": [
            "@commitlint/config-conventional"
        ]
    },
    "husky": {
        "hooks": {
            "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
        }
    }
}
```

## Configurações do arquivo: .releaserc.json

```JSON
{
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    "@semantic-release/github",
    "@semantic-release/changelog",
    [
      "@semantic-release/npm",
      {
        "npmPublish": false
      }
    ],
    {
      "path": "@semantic-release/git",
      "assets": ["package.json", "package-lock.json", "CHANGELOG.md"],
      "message": "chore(release): ${nextRelease.version} [skip ci]\n\n${nextRelease.notes}"
    }
  ]
}
```

## Configuracoes do Makefile

```bash
include .env

release:
	GITHUB_TOKEN=${GITHUB_TOKEN} yarn release
```
