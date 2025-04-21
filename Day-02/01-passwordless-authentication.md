# How to setup Passwordless Authentication

## EC2 Instances

### Using Public Key

```
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

- ssh-copy-id: This is the command used to copy your public key to a remote machine.
- -f: This flag forces the copying of keys, which can be useful if you have keys already set up and want to overwrite them.
- "-o IdentityFile <PATH TO PEM FILE>": This option specifies the identity file (private key) to use for the connection. The -o flag passes this option to the underlying ssh command.
- ubuntu@<INSTANCE-IP>: This is the username (ubuntu) and the IP address of the remote server you want to access.

Copy the key into WSL’s native filesystem:
```
cp /mnt/c/Users/ganes/Downloads/testkey.pem ~/.ssh/  #cp source-file(downloads in local machine) destination-file(ssh) 
```
Set the correct permissions on the copied file:

chmod 400 ~/.ssh/testkey.pem

Now run ssh-copy-id using the key in your WSL home:

ssh-copy-id -f "-o IdentityFile=~/.ssh/testkey.pem" ubuntu@<INSTANCE-PUBLIC-IP>

Then try connecting:

ssh ubuntu@<INSTANCE-PUBLIC-IP>

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`

