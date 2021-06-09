# GitHub Actions Runner 

[![Docker Pulls](https://img.shields.io/docker/pulls/alexbocharov/github-runner.svg)](https://hub.docker.com/r/alexbocharov/github-runner) 

Docker images for GitHub Actions Runner.

## Build Status

| Container Base | amd64 |
| -------------- | ----- |
| ubuntu focal | [![focal-amd64-ci](https://github.com/alexbocharov/github-actions-runner-docker/actions/workflows/focal-amd64-ci.yml/badge.svg)](https://github.com/alexbocharov/github-actions-runner-docker/actions/workflows/focal-amd64-ci.yml) ||

## Full Tag Listing

### Linux Images

| Tags | Architecture | Dockerfile | OS Version |
| ---- | ------------ | ---------- | ---------- |
| github-runner:2.277.1-focal | amd64 | [Dockerfile](./src/focal/amd64/Dockerfile) | Ubuntu 20.04 |
| github-runner:2.278.0-focal | amd64 | [Dockerfile](./src/focal/amd64/Dockerfile) | Ubuntu 20.04 |

## Usage

### Run the Container

To run GitHub Actions Runner container for organization, execute the command:

```
docker run -d --restart always --name github-runner \
  -e RUNNER_NAME="you-runner-name" \
  -e GITHUB_ACCESS_TOKEN="you-github-access-token" \
  -e RUNNER_GROUP="you-runner-group" \
  -e RUNNER_ORGANIZATION_URL="https://github.com/you-org" \
  -e RUNNER_LABELS="you-runner-labels,you-other-runner-labels" \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp:/tmp \
  alexbocharov/github-runner:2.278.0-focal
```

To run GitHub Actions Runner container for repository, execute the command:

```
docker run -d --restart always --name github-runner \
  -e RUNNER_NAME="you-runner-name" \
  -e GITHUB_ACCESS_TOKEN="you-github-access-token" \
  -e RUNNER_GROUP="you-runner-group" \
  -e RUNNER_REPOSITORY_URL="https://github.com/you-repo" \
  -e RUNNER_LABELS="you-runner-labels,you-other-runner-labels" \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /tmp:/tmp \
  alexbocharov/github-runner:2.278.0-focal
```

## Environment variables

The following environment variables allows you to control the configuration parameters.

| Name | Description | Required / Default value |
| ---- | ----------- | ------------------------ |
| RUNNER_NAME | Name of the runner displayed in the GitHub UI | Hostname of the container |
| RUNNER_LABELS | Extra labels in addition to the default: 'self-hosted,Linux,X64' (based on your OS and architecture) | "" |
| RUNNER_WORK_DIRECTORY | Runner's work directory | "_work" |
| RUNNER_REPOSITORY_URL | The runner will be linked to this repository URL | Required if `RUNNER_ORGANIZATION_URL` is not provided |
| RUNNER_ORGANIZATION_URL | The runner will be linked to this organization URL. *(Self-hosted runners API for organizations is currently in public beta and subject to changes)* | Required if `RUNNER_REPOSITORY_URL` is not provided |
| GITHUB_ACCESS_TOKEN | Personal Access Token. Used to dynamically fetch a new runner token (recommended, see below). | Required if `RUNNER_TOKEN` is not provided. |
| RUNNER_TOKEN | Runner token provided by GitHub in the Actions page. These tokens are valid for a short period. | Required if `GITHUB_ACCESS_TOKEN` is not provided |

## License

The Docker Image is available under the MIT license.

[Licensing details](./LICENSE)

## Feedback

Report issues or suggestions in the GitHub Issues.
