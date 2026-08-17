# CLIProxyAPIPlus Releases

This public repository contains release automation and public artifacts for CLIProxyAPIPlus.

The source repository remains private. A read-only deploy key lets trusted scheduled and manually dispatched workflows fetch an exact source tag at build time. Source files are not committed or uploaded to this repository.

## Automation

- `sync-private-tags` checks the private source repository for new version tags every five minutes.
- `release` builds macOS, Windows, Linux, and FreeBSD archives and publishes checksums.
- `docker-image` publishes multi-architecture images to `ghcr.io/davidzhang12138/cli-proxy-api-plus` after a release is published.

The first automatically synchronized version is `v7.2.134`.
