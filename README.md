# GHCR Artifact Action

A lightweight GitHub Action to **upload and download arbitrary files** to/from
**GitHub Container Registry (GHCR)** using **ORAS**.

This allows you to share build artifacts **across repositories**, **across workflows**, and fully **within your organization**, without Docker images, without releases, and without external storage.

---

## 🚀 Features

- Upload any file (ZIPs, binaries, configs, build outputs, etc.)
- Download cross-repository using the built-in `GITHUB_TOKEN`
- Versioned storage using GHCR tags
- No Dockerfiles or container images required
- Multiple files per artifact
- Automatic MIME-type detection
- Pure OCI artifact storage via ORAS
- Works with GitHub Enterprise and GitHub.com

---

## 📦 Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `mode` | Yes | `"upload"` or `"download"` |
| `name` | Yes | Artifact name: `ghcr.io/<org>/<name>` |
| `tag` | No | Artifact tag (default: `latest`) |
| `files` | Upload only | Space-separated file list. Optionally append `:<content-type>` |
| `output` | Download only | Directory to place downloaded files (default: `artifact-out`) |

---

## 🔐 Permissions

Needs `GITHUB_TOKEN` passed as env variable, e.g:

```yaml
- name: Push documentation to ORAS registry
  uses: ./.github/actions/ghcr-artifact
  env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  with:
      mode: upload
      name: runvoy-docs
      tag: latest
      files: gomarkdoc.tar.gz
```

### Upload workflow

```yaml
permissions:
  packages: write
```
