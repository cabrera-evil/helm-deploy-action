# Helm Deploy Action

Welcome to the **Helm Deploy Action** project repository. This project provides a GitHub Action for deploying Helm charts to Kubernetes using a Bash-based CLI tool. It supports local and remote charts, multi-stage environments, and common Helm operations like upgrade, uninstall, and status.

## Table of Contents

- [Helm Deploy Action](#helm-deploy-action)
  - [Table of Contents](#table-of-contents)
  - [Usage](#usage)
  - [Inputs](#inputs)
  - [Supported Commands](#supported-commands)
  - [License](#license)
  - [Contributing](#contributing)

## Usage

To use this GitHub Action in your workflows, include the following step in your `.github/workflows` YAML file:

```yaml
- name: Deploy via Helm
  uses: cabrera-evil/helm-deploy-action@v1
  with:
    command: upgrade
    namespace: dev
    release: my-app
    stage: dev
    dir: ./charts/my-app
    repo: https://cabrera-evil.github.io/charts
    repo-name: evil
    chart: deploy-chart
```

This will execute the `deploy.sh` script internally, using the specified Helm configuration.

## Inputs

The following inputs are supported:

- **`command`** (**required**): One of `install`, `upgrade`, `uninstall`, `status`, `logs`, or `describe`.
- **`namespace`** (_optional_): The Kubernetes namespace (default: `default`). If `stage` is provided, the namespace becomes `default-<stage>`.
- **`release`** (_optional_): The Helm release name (default: `deploy-chart`).
- **`stage`** (_optional_): The deployment stage (e.g., `dev`, `prod`) — this is used to locate `values.<stage>.yaml`.
- **`dir`** (_optional_): The directory containing the Helm chart (default: current directory).
- **`values`** (_optional_): Path to a custom `values.yaml` file (overrides stage-based detection).
- **`repo`** (_optional_): The remote Helm repository URL (e.g., `https://charts.example.com`).
- **`repo-name`** (_optional_): The alias to assign to the remote Helm repo (default: `remote`).
- **`chart`** (_optional_): The name of the chart in the remote Helm repo (required if using `repo`).

## Supported Commands

- `install`: Install the Helm chart
- `upgrade`: Upgrade (or install) the Helm release
- `uninstall`: Remove the Helm release
- `status`: Show the status of the release
- `logs`: Tail logs from the main pod
- `describe`: Describe the main pod in the release

> The script also prints a summary block of what it's doing before executing any Helm command.

## License

This repository is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute as long as you include the original license text.

## Contributing

We welcome and encourage contributions to improve this action. Fork the repository, create a branch, and submit a pull request. All PRs will be reviewed for quality and consistency with the project's scope.
