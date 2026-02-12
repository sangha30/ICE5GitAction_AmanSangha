GitHub Actions: Sequential and Multi-Platform Workflows
Project Overview
This project demonstrates the implementation of automated CI/CD pipelines using GitHub Actions. It consists of two distinct workflows designed to showcase job dependencies, environment configurations, and multi-platform execution.

1. Workflows
Sequential Dependent Jobs (dependent-jobs.yml)
Purpose: Simulates a standard software lifecycle where jobs must occur in a specific order: Build → Test → Deploy.

Trigger: Executes on every push to the master (or main) branch.

Logic: Uses the needs keyword to ensure that the Test job only starts if the Build job succeeds, and the Deploy job only starts if the Test job succeeds.

Multi-Platform Workflow (multi-platform.yml)
Purpose: Demonstrates cross-platform compatibility by running the same logic simultaneously on different operating systems.

Trigger: Executes on pull_request events targeting the master (or main) branch.

Jobs: Runs three independent jobs in parallel:

ubuntu-latest

windows-latest

macos-latest

2. Key Concepts Demonstrated
needs: Used in the first workflow to create a dependency graph. This prevents a deployment from occurring if the previous build or test stages fail.

runs-on: Defines the type of machine (runner) the job executes on. This allowed us to test OS-specific commands like uname -a (Linux/macOS) vs. systeminfo (Windows).

steps & uses: Utilized actions/checkout@v4 to bring the repository code into the runner environment.

Multi-line Commands (|): Used to run multiple shell commands (like echo followed by sleep) within a single step.

3. Challenges & Resolutions

Issue: Workflow not triggering on Pull Request:

Challenge: The workflow was configured to trigger on the main branch, but the repository was using master as the default branch.

Resolution: Updated the YAML configuration's on: pull_request: branches: section to match the actual branch name (master).

Issue: Folder Naming:

Challenge: GitHub did not recognize the workflows initially.

Resolution: Corrected the directory structure from .github/workflow to the plural .github/workflows.
