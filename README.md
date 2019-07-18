## How To Use Vault to Protect Sensitive Ansible Data.

#### Introduction:-
- Ansible Vault is a feature that allows users to encrypt values and data structures within Ansible projects.
 
- This provides the ability to secure any sensitive data that is necessary to successfully run Ansible plays but should not be publicly visible, like passwords or private keys. 

- Ansible automatically decrypts vault-encrypted content at runtime when the key is provided.

In this guide, we will demonstrate how to use Ansible Vault for creating Protect Sensitive Ansible Dataand explore some recommended practices to simplify its use.

#### Prerequisites:-

On the server (Any flavour of UNIX/LINUX System), you will need to install and configure Ansible. You can follow this tutorial on installing [Ansible on Ubuntu 16.04 ](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-16-04 "Ansible on Ubuntu 16.04 ")to install the appropriate packages.

Continue with this guide when your server is configured with the above requirements.

### What is Ansible Vault?
Ansible Vault is a feature of ansible that allows you to keep sensitive data such as passwords or keys in encrypted files, rather than as plaintext in playbooks or roles.

It uses the AES256 algorithm to provide symmetric encryption keyed to a user-supplied password. This means that the same password is used to encrypt and decrypt content, Ansible is able to identify and decrypt any vault-encrypted files it finds while executing a playbook or task.

###### In our case we use ansible-vault concept for encrypt strings( That may be password, variable, name, etc...)

#### Use encrypt_string to create encrypted variables to embed in yaml.
 The *ansible-vault encrypt_string* command will encrypt and format a provided string into a format that can be included in ansible-playbook YAML files.
 
##### To encrypt a string use bellow command.
###### #Syntax:
``ansible-vault encrypt_string``
###### #Output:
![](https://gitlab.rosetta.ericssondevops.com/mela-esn-bss/bscs-nk-api/blob/dev-branch/.devops/images_readme/encryption_string1.PNG)


``ansible-vault encrypt_string --vault-password-file a_password_file 'foobar' --name 'the_secret'``