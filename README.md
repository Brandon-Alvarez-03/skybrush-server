# Skybrush Server Setup Guide for macOS

This guide provides a comprehensive step-by-step process to set up the Skybrush server on macOS.

## Table of Contents

1. [Install Homebrew](#install-homebrew)
2. [Install Python](#install-python)
3. [Verify Python Installation](#verify-python-installation)
4. [Install pip](#install-pip)
5. [Install penv (Optional)](#install-penv-optional)
6. [Clone the Skybrush Server Repository](#clone-the-skybrush-server-repository)
7. [Create a Virtual Environment](#create-a-virtual-environment)
8. [Activate the Virtual Environment](#activate-the-virtual-environment)
9. [Install Poetry (Temporary Step)](#install-poetry-temporary-step)
10. [Generate Requirements File](#generate-requirements-file)
11. [Install Dependencies](#install-dependencies)
12. [Run the Skybrush Server](#run-the-skybrush-server)
13. [Optional: Uninstall Poetry](#optional-uninstall-poetry)
14. [Additional Configurations](#additional-configurations)
    - [Configuration Files](#configuration-files)
    - [Running the Server with Configuration](#running-the-server-with-configuration)
15. [File Structure](#file-structure)
16. [Important Notes](#important-notes)

## Install Homebrew

Homebrew is a package manager for macOS. If you don't have it installed, you can install it by running the following command in your terminal:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Install Python

Once Homebrew is installed, you can use it to install Python:

```bash
brew install python
```

## Verify Python Installation

Ensure Python is installed correctly by checking the version:

```bash
python3 --version
```

## Install pip

pip should come pre-installed with Python. Verify pip installation:

```bash
pip3 --version
```

If pip is not installed, you can install it using the following command:

```bash
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
```

## Install penv (Optional)

You can use penv for virtual environment management if you prefer:

```bash
pip3 install penv
```

## Clone the Skybrush Server Repository

Clone the repository to your local machine:

```bash
git clone https://github.com/Brandon-Alvarez-03/skybrush-server.git
cd skybrush-server
```

## Create a Virtual Environment

Create a virtual environment using the built-in `venv` module:

```bash
python3 -m venv .venv
```

## Activate the Virtual Environment

Activate the virtual environment:

```bash
source .venv/bin/activate
```

## Install Poetry (Temporary Step)

Install `poetry` to manage dependencies:

```bash
pip install poetry
```

## Generate Requirements File

Use `poetry` to export the dependencies to a `requirements.txt` file:

```bash
poetry export -f requirements.txt --output requirements.txt --without-hashes
```

## Install Dependencies

Install the dependencies listed in the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

## Run the Skybrush Server

Start the Skybrush server using the following command:

```bash
PYTHONPATH=src python -m flockwave.server.launcher
```

## Optional: Uninstall Poetry

If you want to remove `poetry` after generating the requirements file:

```bash
pip uninstall poetry
```

## Additional Configurations

### Configuration Files

You can use the provided configuration files (`skybrush-outdoor.jsonc` or `skybrush-virtual.jsonc`) to configure the server. Place these files in the appropriate directory and ensure the server is pointing to the correct configuration file.

### Running the Server with Configuration

If you need to specify a configuration file, you can do so by modifying the command to include the path to your configuration file:

```bash
PYTHONPATH=src python -m flockwave.server.launcher --config etc/conf/skybrush-outdoor.jsonc
```

## File Structure

Here is the essential file structure for the Skybrush server setup:

```
skybrush-server/
├── .venv/
├── CHANGELOG.md
├── DEPENDENCIES.md
├── LICENSE.txt
├── README.md
├── doc/
│   └── make.py
├── etc/
│   ├── conf/
│   │   ├── skybrush-outdoor.jsonc
│   │   └── skybrush-virtual.jsonc
│   └── deployment/
│       ├── docker/
│       │   ├── amd64/
│       │   │   └── Dockerfile
│       │   └── build.sh
│       └── rpi/
│           ├── collmot-init.service
│           ├── network.cfg
│           ├── run-tasks-at-boot
│           ├── skybrush-console-frontend.json
│           ├── skybrush.json
│           ├── tty1-override.conf
│           └── ufw.conf
├── poetry.lock
├── poetry.toml
├── pyproject.toml
├── pytest.ini
├── requirements.txt
├── src/
│   └── flockwave/
│       ├── gateway/
│       │   ├── __init__.py
│       │   ├── app.py
│       │   ├── asgi_app.py
│       │   ├── config.py
│       │   ├── errors.py
│       │   ├── launcher.py
│       │   ├── logger.py
│       │   ├── version.py
│       │   └── workers.py
│       ├── proxy/
│       │   ├── __init__.py
│       │   ├── app.py
│       │   ├── config.py
│       │   ├── launcher.py
│       │   ├── logger.py
│       │   ├── version.py
│       └── server/
│           ├── __init__.py
│           ├── __main__.py
│           ├── app.py
│           ├── comm.py
│           ├── command_handlers/
│           ├── commands.py
│           ├── config.py
│           ├── errors.py
│           ├── ext/
│           ├── launcher.py
│           ├── logger.py
│           ├── message_handlers.py
│           ├── message_hub.py
│           ├── middleware/
│           ├── model/
│           ├── ports.py
│           ├── registries/
│           ├── show/
│           ├── tasks/
│           ├── types.py
│           ├── utils/
│           └── version.py
└── test/
    ├── fixtures/
    ├── test_crazyflie_trajectory.py
    ├── test_ext_show_clock_synchronization.py
    ├── test_led_lights_task.py
    ├── test_mission.py
    ├── test_model.py
    ├── test_preflight_check.py
    ├── test_progress_reporter.py
    ├── test_rate_limiters.py
    ├── test_show_formats.py
    ├── test_show_player.py
    ├── test_show_rth_plan.py
    ├── test_show_trajectory.py
    ├── test_show_utils.py
    ├── test_show_yaw_control.py
    └── test_utils_formatting.py
```

## Important Notes

- Ensure that the virtual environment is activated before running any Python commands.
- Configuration files (`skybrush-outdoor.jsonc` and `skybrush-virtual.jsonc`) are essential for specifying the server's setup. Place these files in the appropriate directory and reference them correctly when starting the server.
- If using Docker for deployment, follow the provided scripts and Dockerfiles in the `etc/deployment/docker` directory.

By following these instructions, you and your employees should be able to set up and run the Skybrush server on your macOS machines without issues. If you encounter any problems or need further assistance, feel free to ask!
