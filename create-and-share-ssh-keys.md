### CREATE AND SHARE SSH KEYS

### OpenSSH setup
- Install openssh on RedHat based systems: `sudo yum –y install openssh-server openssh-clients`
- Install openssh on Debian based systems: `sudo apt install oppenssh-server`
- To start ssh: `sudo systemctl start sshd`
- To check ssh status: `sudo systemctl status sshd`
- To stop ssh: `systemctl stop sshd`
- To enable ssh to start automatically after each system reboot by using the systemctl command: `sudo systemctl enable sshd`
- To disable ssh persistence after reboot enter: `sudo systemctl disable sshd`

##### Create a hosts file of servers you want to repeatedly log into so you dont have to enter IP addresses every time
- Change to ssh directory: `cd .ssh`
- Open vi and add the host data:
- `vi config`
- `Host server1`
- `HostName [ip address]`
- `User root`
- `Port 22`
- Then save and exit

##### Ssh server configuration is needed to harden server security. The most common settings to enhance security are changing the port number, disabling root logins, and limiting access to only certain users. To edit these settings access the /etc/ssh/sshd_config file: `sudo vim /etc/ssh/sshd_config`
##### Disabling root logins and editing the default port number are good places to start.
- Disable root login: `PermitRootLogin no`
- Change the SSH port to run on a non-standard port. For example: `Port 2002`
- 
##### Save the file after edits and restart sshd: `service ssh resart`
- To access a remote host type: `ssh ipaddress` or `ssh username@ipaddress`.
- Logging in to a remote machine with `ssh ipaddress' the remote machine will assume you intend to use the same username you are currently logged in as.
- Logging in as `ssh username@ipaddress` you will be prompted for the password of the user you are attempting to login as.

##### Setup key based authetication.
- Create a public key on the first server: `ssh-keygen -t rsa -b 4096` OR `ssh-keygen -t ed25519`
- System asks for password, provide it.
- Move to ssh directory and list the files there: `cd .ssh` and `ls -la`
- Give only yourself the permissions to access and use this file: `chmod 700 .ssh`
- Move the PUBLIC KEY to the target server option 1:  `ssh-copy-id -i id_rsa.pub SERVERNAME OR IP`
- Move the PUBLIC KEY to the target server option 2: `scp .ssh/id_rsa.pub {destination} username@IPaddress:/path/to/file` 
- System asks for the password, provide it. 
- Check to make sure it works: `ssh {username}@{servername or IP}`. Enter password for key authentication when prompted. And now we should be on the other server.
- To verify type: `ip a s` displays ip address of the target server you are logged into 
- Now to make sure that everything is in order, check the authorized keys file: cat .ssh/authorized_keys. Should show a huge public key.

##### Advanced ssh with agents
- Agents allow us to ssh into the remote target machine without typing the passphrase every time. This is super convenient but also dangerous.
- `ssh-agent bash` then `ssh-add` This will prompt for the password.
- Now to ssh into remote servers just use `ssh server2` or whatever server names is in the known_hosts file

##### Configure SSH to be more secure
- Login to the remote machine
- `vi /etc/sh/ssh/sshd_config`
- Scroll down to the line that reads `PermitRootLogin yes` and uncomment the line and change the yes part to `without-password`. This ensures that you can only connect if you have preshared the key as root. 
- Save and exit.
- Restart the ssh service: `systemctl restart sshd`
- Type: `exit`
- Now double check with: `ssh servername`
- Should allow login with no password prompt 
- No need to authenticate !
