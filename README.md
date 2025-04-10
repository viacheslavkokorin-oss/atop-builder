# 📦 Atop Package Builder

This repository contains a GitHub Actions workflow to build [atop](https://www.atoptool.nl/) as both `.deb` and `.rpm` packages using Docker.  
The workflow is manually triggered and accepts a version input.

## 🚀 Features

- Builds `.deb` and `.rpm` packages from separate Dockerfiles
- Parallel build jobs for faster execution
- Manual trigger with version input
- Artifacts are stored as downloadable build outputs

## 🧰 Requirements

- Dockerfiles must be present at:
  - `Dockerfile.deb` for Debian-based package build
  - `Dockerfile.rpm` for RPM-based package build
- Each Dockerfile must:
  - Accept a `build-arg` named `ATOP_VERSION`
  - Place the built package(s) in `/build` inside the container

## 🛠️ Usage

To build atop packages:

1. Go to the **Actions** tab in your GitHub repository.
2. Select the workflow: **📦 Build Atop Linux Packages (.deb & .rpm)**.
3. Click **Run workflow**.
4. Enter the version number to build (e.g., `2.11.1`).
5. Click **Run workflow** to start the job.

After the build finishes, you can download the generated `.deb` and `.rpm` files from the "Artifacts" section of the workflow run.

## 🗂️ Output

- `atop-<version>_amd64.deb`: contains the built `.deb` file(s)
- `atop-<version>-1.el8.x86_64`: contains the built `.rpm` file(s)

## 💡 Notes

- The build jobs are completely isolated using Docker — no atop or its dependencies are installed on the host.
- You can further extend this workflow to automatically upload the built packages to an internal Pulp repository if desired.

## Author

- Chris van Meer <chris@atcomputing.nl>
