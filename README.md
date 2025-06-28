# 📦 Atop Package Builder

This repository contains a GitHub Actions workflow to build [atop](https://www.atoptool.nl/) as both `.deb` and `.rpm` packages using Docker.  
The workflow is manually triggered and accepts a version input.

## 🚀 Features

- Builds `.deb` and `.rpm` packages from separate Dockerfiles
- Multi-architecture builds for both amd64 and arm64
- Parallel build jobs for faster execution
- Manual trigger with version input
- Artifacts are stored as downloadable build outputs

## 🧰 Requirements

- Dockerfiles must be present at:
  - `Dockerfile.deb` for Debian-based package build
  - `Dockerfile_el8.rpm` for RPM-based package build for EL8
  - `Dockerfile_el9.rpm` for RPM-based package build for EL9
  - `Dockerfile_el10.rpm` for RPM-based package build for EL9
- Each Dockerfile must:
  - Accept a `build-arg` named `ATOP_VERSION`

## 🛠️ Usage

To build atop packages:

1. Go to the **Actions** tab in your GitHub repository.
2. Select the workflow: **📦 Build Atop Linux Packages (.deb & .rpm)**.
3. Click **Run workflow**.
4. Enter the version number to build (e.g., `2.12.0`).
5. Click **Run workflow** to start the job.

After the build finishes, you can download the generated `.deb` and `.rpm` files from the "Artifacts" section of the workflow run.

## 🗂️ Output

| File Name                           | Platform       | Architecture | Type   |
| ----------------------------------- | -------------- | ------------ | ------ |
| `atop-<version>_amd64.deb`          | Debian         | amd64        | `.deb` |
| `atop-<version>_arm64.deb`          | Debian         | arm64        | `.deb` |
| `atop-<version>-1.el8.aarch64.rpm`  | EL8 (RHEL 8)   | aarch64      | `.rpm` |
| `atop-<version>-1.el8.x86_64.rpm`   | EL8 (RHEL 8)   | x86_64       | `.rpm` |
| `atop-<version>-1.el9.aarch64.rpm`  | EL9 (RHEL 9)   | aarch64      | `.rpm` |
| `atop-<version>-1.el9.x86_64.rpm`   | EL9 (RHEL 9)   | x86_64       | `.rpm` |
| `atop-<version>-1.el10.aarch64.rpm` | EL10 (RHEL 10) | aarch64      | `.rpm` |
| `atop-<version>-1.el10.x86_64.rpm`  | EL10 (RHEL 10) | x86_64       | `.rpm` |

## 💡 Notes

- The build jobs are completely isolated using Docker — no atop or its dependencies are installed on the host.
- You can further extend this workflow to automatically upload the built packages to an internal Pulp repository if desired.
- There is an [Ansible role for atop](https://github.com/chrisvanmeer/ansible-role-atop) available.

## Author

- Chris van Meer - <chris@atcomputing.nl>
