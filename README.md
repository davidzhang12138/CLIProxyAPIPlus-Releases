# CLIProxyAPIPlus Releases

This public repository hosts the release automation for CLIProxyAPIPlus. It does not contain private source code, and **no Releases are stored here**.

## Release flow

- `sync-private-tags` reads version tags from the private source repository every 5 minutes and dispatches a `release` run for every tag that has not been published yet. A specific tag can also be published immediately via manual dispatch.
- `release` checks out the exact private source tag, builds macOS, Windows, Linux (glibc and no-plugin), and FreeBSD archives, then creates the GitHub Release **in the private source repository** together with all archives and `checksums.txt`.
- `docker-image` is dispatched manually for a tag, builds `linux/amd64` and `linux/arm64` images, pushes them to `ghcr.io/davidzhang12138/cli-proxy-api-plus`, and records a `<tag>-docker` marker Release in the private source repository.

Private source is only checked out temporarily on trusted GitHub-hosted runners. It is never committed to this repository, and workflows do not use GitHub Actions/Docker build caches, SBOM, or provenance attestations.

Cross-repository writes (creating Releases and uploading assets in the private source repository) require a PAT with `contents: write` on the source repository, stored as the `MAIN_REPO_TOKEN` secret. Read access to the private source is provided by the `SOURCE_DEPLOY_KEY` deploy key.

## Container image

```text
ghcr.io/davidzhang12138/cli-proxy-api-plus:<version>
ghcr.io/davidzhang12138/cli-proxy-api-plus:latest
```

The first automatically synchronized version is `v7.2.134`.
