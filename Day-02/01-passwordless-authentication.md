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

### Using Password 

- Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`  (Go using sudo nano OR Vim)  ==> Once inside ==> Make "PasswordAuthentication yes"
- Update `PasswordAuthentication yes`
- Restart SSH -> `sudo systemctl restart ssh`


### IF YOU'RE NOT USING EC2 INSTAANCE THEN
- Go to `sudo /etc/shh/
- Here you see `ssh_config` and `sshd_config` files
- Go to `sudo vim /etc/ssh/sshd_config`    ==> - Update or Uncomment `PasswordAuthentication yes`
