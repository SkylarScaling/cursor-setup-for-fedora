# cursor-setup-for-fedora
This repo contains Ansible automation that will install Cursor on Fedora.

# Fedora Workstation Setup: Ansible & Cursor IDE

This repository contains an Ansible playbook designed to bootstrap a Fedora Linux machine for an Infrastructure-as-Code (IaC) workflow. It sets up the environment to use IntelliJ IDEA as the primary Git/project hub, alongside the Cursor AI IDE for advanced generative playbooks.

## What This Playbook Does

Running `setup-workstation.yml` automates the following tasks:
* Installs core dependencies (`git`, `ansible`, `ansible-lint`, `curl`, `wget`, `fuse`).
* Creates a local `~/Applications` directory.
* Downloads the latest Linux AppImage for the Cursor AI IDE.
* Makes the Cursor AppImage executable.
* Generates a `.desktop` shortcut so Cursor appears natively in the Fedora application launcher.

## Prerequisites

Because this is an Ansible playbook, you must install Ansible on your Fedora machine before you can run it. 

Open your terminal and run this bootstrap command:
```bash
sudo dnf update -y && sudo dnf install ansible -y
```

## How to Run the Playbook

Since the playbook uses the `dnf` package manager, it requires administrative privileges.

1. Clone this repository (or download the `setup-workstation.yml` file).
2. Open your terminal and navigate to the directory containing the playbook.
3. Run the playbook with the "Ask for become password" flag (`-K`):
```bash
ansible-playbook setup-workstation.yml -K
```


4. Enter your system `sudo` password when prompted.

## Post-Installation Steps

Some configurations are best done interactively or are specific to your personal IDE profile. Once the playbook finishes successfully, complete these final manual steps:

**1. Generate GitHub SSH Keys**

To push and pull from GitHub without password prompts, generate an SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Output the key using `cat ~/.ssh/id_ed25519.pub` and add it to your GitHub account under **Settings > SSH and GPG keys**.

**2. Configure IntelliJ IDEA**

* Open IntelliJ IDEA and go to **File > Settings > Plugins**.
* Search for and install **Ansible Lint** (for standard YAML/Ansible linting).
* Search for and install **Launch in Cursor** (or "Open in Cursor"). This allows you to right-click any playbook in IntelliJ and instantly jump into Cursor for AI generation.
