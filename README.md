# My simple Ansible settings

## Following setup required to use this playbook:

- Create an inventory file. An example below:
```
$ cat inventory_my.ini
[development]
java_development ansible_host=192.168.100.100 ansible_user=me_user
```

- Create an encrypted vault file with the name _**development_vault_encrypted.yml**_ referenced in this playbook
  - Use the following command
  
   ```
   $ ansible-vault create development_vault_encrypted.yml 
   New Vault password: Enter a memorable_secure_vault_password here
   Confirm New Vault password: <Repeat the above password>
   ```

  - An editor will open. Create the referenced variable in this playbook. That is:
   ```
   development_host_sudo_password: <Enter the sudo password on the target machines>
   ```

  - Optionally, save the password to the vault in a secure text file:
      ```
      echo "memorable_secure_vault_password" > vault_password.txt
      chmod u+rw-x,g-rwx,o-rwx vault_password.txt
      ```

## Now, run the playbook like so:

### Option #1:
Use the following command:

   ```
   ansible-playbook -i inventory_my.ini --ask-vault-pass development.playbook.yml 
   ```
   Enter the vault password when prompted.


### Option #2:
If the vault_password.txt was created like mentioned in the optional setup step above, then use the following command:
```
ansible-playbook -i inventory_my.ini --vault-password-file vault_password.txt development.playbook.yml 
```


