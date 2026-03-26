# Shared GitHub Workflows

Reusable GitHub Actions workflows for jokep86 repositories.

## Available Workflows

### Docker Build and Push - DockerHub (`docker-build-push-dockerhub.yml`)

Builds a Docker image and pushes it to DockerHub. Tags are automatically determined by branch:
- `main` → `release-<sha>`
- any other branch → `development-<sha>`

**Inputs**

| Name | Required | Default | Description |
|---|---|---|---|
| `dockerhub-image` | yes | — | DockerHub image name (e.g. `myusername/myimage`) |
| `environment` | yes | — | GitHub environment name (e.g. `production`, `staging`) |
| `docker-platform` | no | `linux/amd64` | Docker build platform |

**Secrets**

| Name | Required | Description |
|---|---|---|
| `dockerhub-username` | yes | DockerHub username |
| `dockerhub-token` | yes | DockerHub access token |
| `github-packages-token` | no | GitHub packages token for private dependencies |

**Usage**

```yaml
jobs:
  docker:
    uses: jokep86/shared-github-workflows/.github/workflows/docker-build-push-dockerhub.yml@main
    with:
      dockerhub-image: myusername/myimage
      environment: production
    secrets:
      dockerhub-username: ${{ secrets.DOCKERHUB_USERNAME }}
      dockerhub-token: ${{ secrets.DOCKERHUB_TOKEN }}
```

## Setup

Each consuming repository needs:
- `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` secrets set under *Settings → Secrets and variables → Actions*
- A `Dockerfile` at the repo root (or adjust the build context as needed)

## Versioning

Pin to `@main` for latest, or a specific tag for stability:

```yaml
uses: jokep86/shared-github-workflows/.github/workflows/docker-build-push-dockerhub.yml@v1
```
