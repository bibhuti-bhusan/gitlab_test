## HOW TO USE VAULT TO PROTECT SENSITIVE ANSIBLE DATA.

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
#
#### Use encrypt_string to create encrypted variables to embed in yaml.
 The *ansible-vault encrypt_string* command will encrypt and format a provided string into a format that can be included in ansible-playbook YAML files.
 
##### To encrypt a string use bellow command using password.
###### #Syntax:
```sh ansible-vault encrypt_string ```
###### #Output:
![](https://gitlab.rosetta.ericssondevops.com/mela-esn-bss/bscs-nk-api/blob/dev-branch/.devops/images_readme/encryption_string1.PNG)
 Here it will ask the password to encrypt the string and also use this password to decrypt the string.
 
##### To encrypt a string use bellow command using password file in single command.
###### #Create sample password file for encrypting strings.
Create a password file *passwd.txt* for encrypting string and use this file in the command.
###### #Syntax:
``ansible-vault encrypt_string --vault-password <password_file> <'string_to_encrypt'> --name <'string_variable_name'>``
###### #Example
```sh
ansible-vault encrypt_string --vault-password passwd.txt 'NK-API' --name 'product'
```
###### #Output:
![](./images_readme/encryption_string2.PNG)
###### #This above commands are describes how to create encrypted strings.
#
----------
## How to create and copy encrypted values to this *encrypted_values.txt* file in GitLab, follow these steps : 
##### for example if you want change in dev environment (*nk_api_dev_env*)  
Go to [.devops/nk_api_dev_env](.devops/nk_api_dev_env)
1. Copy/download the *passwd* file.
2. Use this command to create encrypted string by using *passwd* file.
    ```sh
    ansible-vault encrypt_string --vault-password <path_of_passwdfile> '<string_to_encrypt>' --name '<string_variable_name>'
    ```
    example:
    ```sh
    ansible-vault encrypt_string --vault-password passwd 'BSCSNKD' --name 'V_DB_NAME_BSCS'
    ```
3. copy output of above command to [.devops/nk_api_dev_env/encrypted_values.txt](.devops/nk_api_dev_env/encrypted_values.txt) this file.
4. and commit the file.

##### Same way for change in any environment
Go to [.devops](.devops) directory, go to any environment and follw above steps.
# END


