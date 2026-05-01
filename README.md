# 🛠️ prox-k8s-lab - Build your own private Kubernetes server

[![](https://img.shields.io/badge/Download-Project-blue)](https://github.com/Proverbial-genicularvein571/prox-k8s-lab)

This project helps you create a private Kubernetes laboratory on Proxmox virtual machines. It automates server setup using Ansible and keeps your applications updated with ArgoCD and Helm. Use this to manage your home media server, storage tools, or test web applications in a private environment.

## 📋 System Requirements

Before you begin, ensure your hardware meets these standards.

* Processor: Modern CPU with virtualization support enabled in the BIOS.
* Memory: 16GB RAM minimum, 32GB recommended for multiple services.
* Storage: 100GB of free space on an SSD.
* Network: A stable wired connection to your router.
* Software: Proxmox Virtual Environment installed on your host machine.
* Operating System: Windows 10 or Windows 11.

## 🚀 Downloading the Files

You get the latest version of the toolkit from the main repository page.

[Click here to visit the download page](https://github.com/Proverbial-genicularvein571/prox-k8s-lab)

Follow these steps to obtain the source code:

1. Open the link above in your web browser.
2. Locate the green button labeled Code.
3. Select Download ZIP from the dropdown menu.
4. Save the file to your desktop.
5. Right-click the downloaded folder and select Extract All.

## ⚙️ Initial Setup

The setup relies on a clean Windows environment. Ensure you have the Windows Subsystem for Linux enabled, as the automation tools run best within an Ubuntu environment.

1. Open PowerShell as an administrator.
2. Type `wsl --install` and press Enter.
3. Restart your computer.
4. Complete the Ubuntu setup by creating a username and password when prompted.
5. Open the Ubuntu terminal application.
6. Install the necessary tools by typing: `sudo apt update && sudo apt install ansible git`.

## 🖥️ Configuring Proxmox

Your Proxmox environment requires specific settings to communicate with the automation scripts.

1. Log into your Proxmox web interface.
2. Create three virtual machines with at least 4GB of RAM each.
3. Ensure these machines run a supported Linux distribution like Debian or Ubuntu Server.
4. Note the IP addresses for each virtual machine.
5. Create a dedicated user on the Proxmox host for the automation tasks and provide it with Administrator permissions.

## 🔑 Security and Access

Automation requires a secure way to access your virtual machines without typing passwords. SSH keys provide this functionality.

1. In your Ubuntu terminal, type `ssh-keygen`.
2. Follow the prompts and press Enter for the default settings.
3. Copy your public key to your Proxmox virtual machines using the command `ssh-copy-id user@your-vm-ip`.
4. Replace `user` with your username and `your-vm-ip` with the actual IP address of your machine.
5. Repeat this process for every virtual machine in your lab.

## 🛠️ Running the Automation

The Ansible playbooks perform the heavy lifting of installing Kubernetes and related tools.

1. Navigate to the extracted folder in your Ubuntu terminal: `cd Desktop/prox-k8s-lab-main`.
2. Open the file named `hosts.ini` using a text editor.
3. Replace the placeholder IP addresses with the IP addresses of your virtual machines.
4. Save your changes.
5. Run the primary installation script: `ansible-playbook setup.yml`.
6. Watch the terminal as it installs Docker, Kubeadm, and prepares the cluster environment.

## 🌐 Deploying Applications

Once the cluster is ready, use ArgoCD and Helm to manage your home services like Plex or Jellyfin.

1. Open your web browser and navigate to the ArgoCD dashboard at `https://your-master-node-ip`.
2. Create a new project for your media server.
3. Link your GitHub repository if you want to track configuration changes automatically.
4. Use Helm charts to deploy applications. Each chart acts as a recipe for a container.
5. Enter the commands provided in the `charts` folder of the repository to begin deployment.

## 📈 Monitoring your Lab

Kubernetes provides tools to watch your services.

1. Install the Kubernetes dashboard to see a visual map of your cluster.
2. Check the logs if a service fails to start.
3. Use the command `kubectl get pods -A` to list every active service in your network.
4. Review resource usage to ensure your Proxmox virtual machines have enough memory and CPU available.

## 🔧 Troubleshooting Common Issues

If a service fails to connect, start with these checks.

* Verify that all virtual machines are powered on and reachable via ping.
* Check that your SSH keys remain valid on all nodes.
* Ensure your Proxmox firewall does not block traffic between the virtual machines.
* Re-run the Ansible playbook to correct any configuration drift.

## 📦 Maintenance Tips

Keep your lab running well with these standard tasks.

* Update your virtual machines regularly using `apt upgrade`.
* Sync your local code repository with the main project page to receive performance improvements.
* Monitor your SSD storage levels to prevent data loss.
* Back up your configuration files to a secondary drive.

## 💡 Using Your Media Server

After installing Plex or Jellyfin:

1. Point the application to your storage directory on the host machine.
2. Adjust your GPU passthrough settings in the Proxmox hardware menu for better video performance.
3. Set up the library paths within the application browser interface.
4. Connect your client devices to the network and locate the server.

You now have a functional Kubernetes lab. You can expand this setup by adding more nodes or deploying additional services as your needs grow. Always keep a backup of your configuration files before changing settings in the cluster.