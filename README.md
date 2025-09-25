# My simple Ansible settings

The purpose of this exercise is to learn ansible while putting it to use in my own homelab.

Git logs will also document my improvement journey as this repo will grow from naive compilation of tasks to adopting known best practices.

###  **[TODO: FOLLOWING INSTRUCTIONS NEEDS A REWRITE AFTER RECENT CHANGES]**

## Following setup required to use this playbook:

- Create an inventory file. An example below:
```
$ cat inventory_ansible.ini
[development]
development_host_name_1 ansible_host=192.168.100.100 ansible_user=user_one
development_host_name_2 ansible_host=192.168.100.101 ansible_user=user_two
```

- Create an encrypted vault file with the name _**development_vault_encrypted.yml**_ referenced in this playbook
  - Use the following command
  
   ```
   $ ansible-vault create development_vault_encrypted.yml 
   New Vault password: any_memorable_secure_vault_password
   Confirm New Vault password: <Repeat the above password>
   ```

  - An editor will open. Create the variable _**development_host_sudo_password**_ referenced in this playbook. Save and close the file.

     The example line in the vault file:
     ```
      development_host_sudo_password: <Enter the sudo password on the target machines>
     ```

  - Optionally, save the password to the vault in a secure text file:
      ```
      $ echo "any_memorable_secure_vault_password" > vault_password.txt
      $ chmod u+rw-x,g-rwx,o-rwx vault_password.txt
      ```

## Now, run the playbook like so:

### Option #1:
Use the following command:

   ```
   ansible-playbook --ask-vault-pass development.playbook.yml
   ```
   Enter the vault password when prompted.


### Option #2:
If the vault_password.txt was created like mentioned in the optional setup step above, then use the following command:
```
ansible-playbook --vault-password-file vault_password.txt development.playbook.yml
```