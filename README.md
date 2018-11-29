# Ansible : Playbook Logstash

The aim of this project is to deploy Logstash on Vagrant instances.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to run this Ansible playbook :

*   [Vagrant](https://www.vagrantup.com/docs/installation/) must be installed on your computer
*   Update the Vagrant file based on your computer (CPU, memory), if needed
*   Update the operating system to deploy in the Vagrant file (default: Ubuntu)
*   Download the Ansible requirements:

```bash
$ ansible-galaxy install -r requirements.yml
```

### Usage

A good point with Vagrant is that you can create, update and destroy all architecture easily with some commands.

Be aware that you need to be in the Vagrant directory to be able to run the commands.

#### Baremetal Deployment

To deploy the Logstash client on baremetal, you have to configure the variable *logstash_on_baremetal* to *true* in the file logstash.yml before running the playbook :

```yaml
[...]
vars:
  logstash_on_baremetal: true
  logstash_on_docker: false
  logstash_on_kubernetes: false
[...]
```

Once it's done, you just have to provision the Vagrant instance and the Ansible playbook will automatically be called :

```bash
$ vagrant up
```

If everything run has expected, you should deploy pipeline files in /opt/logstash/pipeline to manage logs.

#### Docker Deployment

To deploy the Logstash client on Docker, you have to configure the variable *logstash_on_docker* to *true* in the file logstash.yml before running the playbook :

```yaml
[...]
vars:
  logstash_on_baremetal: false
  logstash_on_docker: true
  logstash_on_kubernetes: false
[...]
```

Once it's done, you just have to provision the Vagrant instance and the Ansible playbook will automatically be called :

```bash
$ vagrant up
```

If everything run has expected, you should have a Docker container named logstash which search pipeline files in the host directory : /opt/logstash/pipeline

#### Kubernetes Deployment

To deploy the Logstash client on Kubernetes, you have to configure the variable *logstash_on_kubernetes* to *true* in the file logstash.yml before running the playbook :

```yaml
[...]
vars:
  logstash_on_baremetal: false
  logstash_on_docker: false
  logstash_on_kubernetes: true
[...]
```

Once it's done, you just have to provision the Vagrant instance and the Ansible playbook will automatically be called :

```bash
$ vagrant up
```

If everything run has expected, you should have a namespace and a pod named logstash. This pod should be configured by two config map logstash-config and logstash-pipeline.

#### Destroy

To destroy the Vagrant resources created, just run this command :

```bash
$ vagrant destroy
```

### How-To

This section list some simple command to use and manage the playbook and the Vagrant hosts.

#### Update with Ansible

To update the Logstash configuration with Ansible, you just have to run the Ansible playbook logstash.yml with this command :

```bash
$ ansible-playbook logstash.yml
```

#### Update with Vagrant

To update the Logstash configuration with Vagrant, you just have to run provisioning part of the Vagrant file :

```bash
$ vagrant provision
```

#### Connect to Vagrant instance

To be able to connect to a Vagrant instance, you should use the CLI which is configured to automatically use the default SSH key :

```bash
$ vagrant ssh logstash01
```

## Author

Member of Wikitops : https://www.wikitops.io/

## Licence

This project is licensed under the Apache License, Version 2.0. For the full text of the license, see the LICENSE file.
