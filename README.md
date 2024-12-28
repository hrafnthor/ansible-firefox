ansible-firefox
=========

Ansible role for fetching and installing Firefox through various ways.

Requirements / Dependencies
------------

This role requires the Ansible collection `community.general` to be installed on the system.

This role requires the python package `jsonschema` to be installed on the system.

```shell
pip install jsonschema
```

Setup
-----

Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a requirements.yml file in the root directory of the playbook being worked on.

2. Add the following definition inside the requirements.yml file:

```yaml
roles:
- name: hth-firefox
  src: https://github.com/hrafnthor/ansible-vscode.git
  scm: git
collections:
 - name: community.general
````

3. Install the requirements by executing

```yaml
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role `hth-firefox`


Role Variables
--------------

#### Input variables

Values are optional unless marked otherwise.

```
gather_facts	[optional] (boolean)  Indicates if this role should gather facts or rely on present facts.
mozilla
  signing 	[required]
    path 	[required] (string)   The absolute file path to the signing key used by Mozilla. This key can be found at: https://packages.mozilla.org/apt/repo-signing-key.gpg
    force	           (boolean)  Indicates if the signing key should override any other key found.
  priority	           (boolean)  Indicates if this repository should be given priority over any other.
snap		           (boolean)  Indicates if Firefox should be installed from the Snap store. If false and Firefox is installed from the Snap, it will be uninstalled.
esr		           (boolean)  Indicates if Firefox-ESR should be installed from the MozillaTeam PPA (https://launchpad.net/~mozillateam/+archive/ubuntu/ppa). If false and Firefox-ESR is installed, it will be uninstalled.
```


##### Example input:

```yml
firefox:
  gather_facts: false
  mozilla:
    signing:
      path: "/path/to/mozilla/signing/key.gpg"
      force: false
    priority: true
  snap: false
  esr: true
```


Example Playbook
----------------


```yaml
- hosts: all
    vars:
    - firefox:
        gather_facts: false
        mozilla:
          signing:
            path: "/path/to/mozilla/signing/key.gpg"
            force: false
          priority: true
        snap: false
        esr: true
  roles:
  - hth-firefox
```


License
-------

Apache 2.0. See attached license file.

Author Information
------------------

Hrafn Thorvaldsson.
http://www.hth.is
