---
title: Ansible for Windows Configuration Management
permalink: ansible-for-windows-configuration-management
tags: ansible windows infrastructure-as-code
---

Due to the perception that Windows is point-and-click by nature, it often misses out on the configuration management treatment that Linux has enjoyed for many years.
This can lead to Windows system administrators being forced into an endless cycle of manually performing tasks, with an increased risk of error,
and then forgetting to document. But there is another way. One that involves defining configuration as code, avoiding manual changes, and having your configuration management system apply the changes automatically. One way to achieve that is with Ansible.

## What is Ansible?
Ansible is an open-source automation and configuration management tool that offers a convenient and cost-effective solution for managing your infrastructure. It's free to get started with Ansible, making it accessible to users without financial constraints. One of its key advantages is its agentless nature, meaning you don't need to install any software on the servers you wish to manage. Additionally, there is no need to set up a central server for management purposes, as Ansible allows you to execute commands directly from your local machine. With Ansible, you can automate various tasks and processes, enabling efficient configuration management across your systems and applications.
## Why would you want to use Ansible for managing Windows servers?
Using Ansible for managing Windows servers offers several compelling reasons:

### Documentation and repeatability
When managing Windows servers manually, there is a high probability that the actions performed are undocumented, unrepeatable, and untested. By utilizing Ansible, you can define your server configurations as code, which provides self-documentation, repeatability, and testability.

### Overcoming point-and-click
Windows server management is often associated with a point-and-click graphical interface. However, Ansible breaks away from this paradigm and allows for automation, even in Windows environments. It enables you to define and execute tasks programmatically, transforming the way you manage Windows servers and unlocking the benefits of automation.

### Leveraging existing Ansible knowledge
If you are already using Ansible for managing Linux servers, the barrier to entry for using it with Windows servers is low. Since Ansible is platform-agnostic, the knowledge and experience gained from managing Linux servers can easily be applied to Windows servers. This allows for a consistent and unified approach to server management across your infrastructure.

## What can you achieve with Ansible on Windows servers?
When it comes to managing Windows servers with Ansible, there are a wide range of tasks you can accomplish. Here's an overview:

### Software Deployment
Ansible enables you to efficiently get software onto your Windows servers without resorting to poorly secured file shares. This eliminates the need for manual file copying and keeps your security team happy.

### Dependency Installation
Ansible allows you to automate the installation of dependencies required by your applications or services on Windows servers.

### Silent Installations
With Ansible, you can run installers with unattended or silent modes. This means you can provide a configuration file and have the installer execute without requiring any user input.

### Windows Roles and Features
Ansible can handle the installation and configuration of Windows roles and features, enabling you to customize your server environment efficiently.

### Customization
Ansible empowers you to perform various customizations on Windows servers, such as branding, managing configuration files, and ensuring self-documentation. This helps prevent drift from your documented configurations and promotes consistency.

### Extensibility
Ansible provides extensive capabilities for managing Windows servers. You can leverage both standard and community modules specifically designed for Windows, including file management, certificate management, Windows service configuration, registry settings, IIS configuration, firewall configuration, and installation of PowerShell modules.

If you can't find a specific module for a task, Ansible allows you to run commands and execute PowerShell scripts directly on Windows servers, providing flexibility for accomplishing any desired action.

## Automate your Configuration Management
Now that your Windows server configuration is code, you can utilise a CI pipeline to automatically test and deploy that configuration.
To automate the management of Windows servers using Ansible within a Continuous Integration (CI) pipeline, you can follow these general steps:

- Store your Ansible playbooks, roles, and configurations in a version control system, such as Git. This ensures proper versioning, collaboration, and traceability of changes.

- Set up a CI server or platform, such as Jenkins, GitLab CI/CD, or Azure DevOps, where you can define and run your CI pipeline.

- Define a configuration file specific to your CI platform that describes the steps and stages of your pipeline. This file typically includes information such as the repository location, triggered events, and the tasks to be executed.

- Define the necessary stages in your CI pipeline to execute the Ansible tasks. These stages could include building and preparing the environment, executing the Ansible playbooks, and handling any necessary post-processing or cleanup tasks.

- Ensure secure handling of secrets and authentication credentials required for managing Windows servers. This may involve using secure storage solutions or integrating with credential management systems to securely provide access to the target servers.

- Set up proper testing and validation processes within your CI pipeline to ensure that the desired configurations and actions are applied correctly to the Windows servers. This may involve running test scenarios, verifying desired state, and capturing any failures or errors.

- Once the Ansible tasks pass all tests and validation, you can deploy the configurations and changes to your production Windows servers using the CI pipeline's deployment stage. Ensure proper testing and promotion practices to minimize the risk of introducing issues into the production environment.

## Examples
Here are a few example tasks for managing Windows servers using Ansible:

Install a Windows Feature:
```yaml
- name: Install IIS
  win_feature:
    name: Web-Server
    state: present
```

Create a new Windows user:
```yaml
- name: Create user
  win_user:
    name: johndoe
    password: P@ssw0rd
    state: present
    groups: Administrators
```

Configure Windows Firewall:
```yaml
- name: Allow incoming HTTP traffic
  win_firewall_rule:
    name: Allow HTTP
    direction: in
    action: allow
    protocol: tcp
    localport: 80
```

Copy files to Windows Server:
```yaml
- name: Copy files
  win_copy:
    src: /path/to/local/file.txt
    dest: C:\Temp\file.txt
```

Restart Windows Server:
```yaml
- name: Restart server
  win_reboot:
    reboot_timeout: 300
```

Configure a Windows service:
```yaml
- name: Wingding service configuration
  ansible.windows.win_service:
    name: Wingdings
    start_mode: delayed
    failure_actions:
      - type: restart
        delay_ms: 300000 # 5 minutes
      - type: restart
      - type: restart
```

Configure HTTPS binding in IIS:
```yaml
- name: Configure HTTPS Binding for Default Web Site
  community.windows.win_iis_webbinding:
    name: Default Web Site
    protocol: https
    port: 443
    ip: '*'
    certificate_hash: 0123456789abcdef
    state: present
```

## Conclusion
Ansible offers a powerful and flexible solution for managing Windows servers. By adopting Ansible, you can overcome the challenges of manual configuration and documentation, and embrace the benefits of automation and repeatability. With its agentless architecture, Ansible simplifies the management process by eliminating the need for additional software installations. Whether it's deploying software, managing dependencies, customizing configurations, or executing a wide range of tasks, Ansible provides the tools and modules to streamline your Windows server management. By leveraging the existing knowledge and experience gained from using Ansible with Linux servers, you can extend its usage to Windows servers and achieve a consistent and unified approach across your infrastructure. With Ansible, you can transform the way you manage Windows servers, improve efficiency, reduce errors, and bring the power of automation to your Windows environment.