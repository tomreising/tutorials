Step 1: Install OpenSSH
Ensure that OpenSSH is installed on both systems. Most Linux distributions come with OpenSSH pre-installed, but if not, you can install it using the package manager.

# On Debian/Ubuntu
```
sudo apt-get install openssh-server

```
# On Red Hat/Fedora
```
sudo dnf install openssh-server

```
# On CentOS
sudo yum install openssh-server
Step 2: Generate SSH Keys
On each system, generate an SSH key pair if you don't already have one. The following command will generate a new SSH key pair (if not already present):

```
ssh-keygen -t ed25519 -C "your_email@example.com"

```
You can press Enter to accept the default file location (~/.ssh/id_rsa), or change it then press enter (i.e. ~/.ssh/my_rsa_key).
When prompted to provide a password you can simply hit enter but this is less secure.

Step 3: Copy Public Key to Remote System
Use ssh-copy-id to copy the public key to the remote system. Replace user and remote-ip with the username and IP address of the remote system.

```
ssh-copy-id user@remote-ip

```
You'll be prompted to enter the password for the remote user.

Note: You can also manually add it to the remote autherized keys by going into the remote server. Note the .pub file is the key that needs to be added to the remote.
For example go to remote server cd to ~/.ssh and run nano authorized_keys.

```
cd ~/.ssh
nano authorized_keys
```

Step 4: Disable Password Authentication (Optional)
For increased security, you can disable password authentication and rely solely on SSH keys. Edit the SSH configuration file:

```
sudo nano /etc/ssh/sshd_config

```
Find the line PasswordAuthentication and set it to no:
Note: There may be other subfiles or directories with subfiles that may have this setting so confirm they all are set to no
```
PasswordAuthentication no

```
Save the file and restart the SSH service:

```
sudo systemctl restart ssh

```
Step 5: Test SSH Connection
You should now be able to SSH into the remote system without entering a password:

```
ssh user@remote-ip

```
Note: Security Considerations
Always use strong passphrases for your SSH keys if you decide to set one during key generation.
Regularly update and patch your systems to ensure you have the latest security updates.
Consider using a non-default SSH port for an extra layer of security.
If applicable, configure a firewall to allow SSH traffic only from trusted IP addresses.
This simple tutorial provides a basic configuration for SSH. Depending on your security requirements and use case, you may need to explore more advanced configurations and additional security measures.
