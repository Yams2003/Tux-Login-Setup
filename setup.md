# SSH Configurations #
1. Open your SSH configuration file using a text editor. If you are using a Unix-like system, this file should be located at ~/.ssh/config.
If the file doesn't exist, you can create it.
```
vim ~/.ssh/config
```
2. Add an entry for TUX. Replace username with your actual username on TUX. (With the updated TUX this would be your full email like abc123@drexel.edu).
You would need to include the path to your private key file if it is not the default (~/.ssh/id_rsa).
```
Host tux
HostName tux.cs.drexel.edu
User username
IdentityFile ~/.ssh/id_rsa
```
3. Save and close the file. In vim you can close and save the file in command mode with the `wq` command.
4. Now, you should be able to login to TUX by just typing:
```
ssh tux
```
5. Remember that the SSH configuration file and your SSH keys should be kept secure.
6. The permissions for ~/.ssh/config should be set to 600 to ensure that only you can read and write to the file.
```
chmod 600 ~/.ssh/config
```

# Bypassing Password with SSH Keys #

1. First, on your local machine (the machine you are working from), check for existing SSH keys.
You can do this by navigating to your ~/.ssh directory and looking for a pair of files: id_rsa (private key) and id_rsa.pub (public key).
If these files exist and you're confident they aren't being used for another purpose, you can use them. If not, you'll need to generate a new set. You can check this by running the following command:
```
ls -la ~/.ssh
```
2. Generate new SSH keys if necessary. Run the following command:
```
ssh-keygen -t rsa -b 4096
```
You'll be prompted to enter a file in which to save the key. Press `Enter` to accept the default location (.ssh/id_rsa). If you choose a different location, you'll have to specify the key location in your SSH commands.
You'll also be prompted to enter a passphrase. This is an extra layer of security, but for this task, you can leave it empty and just press `Enter`.

3. Copy the public key to the remote machine. This is accomplished with the ssh-copy-id command. 
Replace username with your username on TUX.
```
ssh-copy-id username@tux.cs.drexel.edu
```
You'll be prompted to enter your password for the remote machine. After entering it, your public key will be added to the file ~/.ssh/authorized_keys on the remote machine.
This means that the remote machine will recognize and trust your local machine in the future. If this step does not work with the new tux server, check the step below.

>3<sup>1</sup>&frasl;<sub>2</sub>. Display and copy the your public ssh key using this command:
>```
>cat ~/.ssh/id_rsa.pub
>```
>You should have some sort of output looking like this `ssh-rsa AAAAB3NzaC...yourusername@yourhostname`.
Next, you will log on to the remote tux server and append the public key to the ~/.ssh/authorized_keys file. First, check if the ~/.ssh directory exists. If it doesn't, you'll need to create it:
>```
>mkdir -p ~/.ssh
>```
>The -p flag ensures that mkdir creates the directory and does not throw an error if it already exists.
>Next, open the authorized_keys file in a text editor. You can use nano, vim, or any other text editor. If the file doesn't exist, this command will create it:
>```
>vim ~/.ssh/authorized_keys
>```
>Paste your public key at the end of this file, then save and exit
>Finally, set the permissions of the ~/.ssh directory and the authorized_keys file to ensure that only your user can read and write to them:
>```
>chmod 700 ~/.ssh
>chmod 600 ~/.ssh/authorized_keys
>```
>Now, your public key has been added to the authorized_keys file on the remote server. You should be able to log into the server without a password, just like if you had used `ssh-copy-id`.

4. Now, you can test the new setup by SSH'ing into your remote machine:
```
ssh tux
```
You should be logged in without being prompted for a password.


Remember to protect your private key: anyone who gains access to your private key can SSH into your remote machine without a password. 
Make sure the permissions of your ~/.ssh directory are restrictive (700 is recommended: drwx------), and similarly, the private key file should also have restrictive permissions (600 is recommended: -rw-------).
