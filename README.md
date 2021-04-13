# GitHub Actions Runner 

Docker images for GitHub Actions Runner.

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