# Omni

This repository contains the CI/CD configuration and infrastructure-as-code setup for managing Kubernetes clusters using the **Sidero Omni** platform. All cluster operations, including provisioning, patching, and updates, are automated through GitHub Actions workflows.

## 📁 Project Structure

- `.github/workflows/` – CI/CD pipelines that automate cluster lifecycle management.
- `clusters/` – Definitions and configuration patches for managed clusters (e.g., `khan`, `kronos`).
- `general/` – Shared resources and global configurations (e.g., `MachineClasses`).

## 🚀 Getting Started

> **Note:** This project assumes familiarity with Kubernetes and the Sidero Omni platform.

### Prerequisites

- GitHub Actions (for CI/CD automation)
- Access to Sidero Omni
- The following GitHub Secrets configured in your repository:
  - `OMNI_SERVICE_ACCOUNT_KEY` – Sidero Omni service account credentials.
  - `OMNI_ENDPOINT` – The API endpoint of your Sidero Omni instance.
  - `GITHUB_TOKEN` – Used by GitHub Actions to post PR comments and authenticate with the GitHub API.

## 🧪 Making Changes

To update a cluster or its resources:

1. Edit the appropriate YAML files under `clusters/` or `general/`.
2. Push your changes or open a pull request.
3. Monitor the GitHub Actions pipeline for deployment status.

## 🔄 CI/CD with OmniCTL

Cluster and General configurations are fully automated through GitHub Actions using two workflows:

### OmniCTL - Clusters

- Handles cluster-specific configuration updates under `clusters/`.
- On pushes or pull requests affecting `clusters/**` files:
  - Validates the cluster configuration using `omnictl`.
  - Runs a diff (`plan`) to show the proposed changes to the cluster state.
  - Posts the plan and validation results as a comment on pull requests.
  - Applies changes automatically on push to the `main` branch.

### OmniCTL - General

- Handles shared/global configuration updates under `general/` (e.g., `MachineClasses`).
- On pushes or pull requests affecting `general/**` files:
  - Merges all YAML files into a temporary config file.
  - Validates the combined configuration.
  - Runs a dry-run plan and posts the output as a comment on pull requests.
  - Applies changes automatically on push to the `main` branch.
