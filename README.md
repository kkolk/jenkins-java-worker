# Jenkins Java Worker
This repository contains the ansible playbooks and related files 
for the management of Jenkin's Java worker nodes.

## Overview

This role currently installs the following packages onto the worker node and registers it with the Jenkin's Master:

* Java JDK
* Maven
* Git
* Unzip
* Zip
* bzip2
* Ant

## Jenkins Integration

TBD.

## Java

The Java role is currently fairly straight forward and installs the latest version of OpenJDK on the platform.   This will likely need modification in the near future to use the Oracle JDK.

## Maven

### Role Variables for Maven

Variables are currently all managed through the **all.yml** 
in **inventory/lab/group_vars/java-worker/all.yml**

The following variables will change the behavior of this role 
(sample values are shown below):

```yaml
# Maven version number
maven_version: '3.6.0'

# Mirror to download the Maven redistributable package from
maven_mirror: "http://archive.apache.org/dist/maven/maven-{{ maven_version|regex_replace('\\..*', '') }}/{{ maven_version }}/binaries"

# Base installation directory the Maven distribution
maven_install_dir: /opt/maven

# Directory to store files downloaded for Maven installation
maven_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"

# If this is the default installation, symbolic links to mvn and mvnDebug will
# be created in /usr/local/bin
maven_is_default_installation: yes

# Name of the group of Ansible facts relating this Maven installation.
#
# Override if you want use this role more than once to install multiple versions
# of Maven.
#
# e.g. maven_fact_group_name: maven_3_3
# would change the Maven home fact to:
# ansible_local.maven_3_2.general.home
maven_fact_group_name: maven
```

### Supported Maven Versions

The following versions of Maven are supported without any additional
configuration (for other versions follow the Advanced Configuration
instructions):

* `3.6.0`
* `3.5.4`
* `3.5.3`
* `3.5.2`
* `3.5.0`
* `3.3.9`
* `3.2.5`
* `3.1.1`

Version files are maintained in ***roles\maven\vars\versions\\#.#.#.yml*** if you wish to 
add additional out of the box supported values.

### Advanced Configuration for additional Maven versions

The following role variable is dependent on the Maven version; to use a
Maven version **not listed above** you must configure the
variable below:

```yaml
# SHA256 sum for the redistributable package (i.e. apache-maven-{{ maven_version }}-bin.tar.gz)
maven_redis_sha256sum: '6a1b346af36a1f1a491c1c1a141667c5de69b42e6611d3687df26868bc0f4637'
```

To retrieve the sha256sum for a particular version, download the tar.gz file and then run the following command from within the download directory.

    sha256sum apache-maven-3.6.0-bin.tar.gz 

sha256sum should then print out a single line after calculating the hash:

    6a1b346af36a1f1a491c1c1a141667c5de69b42e6611d3687df26868bc0f4637 *apache-maven-3.6.0-bin.tar.gz

Copy this value into the maven_redist_sha256sum.