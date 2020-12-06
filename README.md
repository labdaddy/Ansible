### Ansible Key Setup
- create ssh key dedicated to this repo: `ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "comment goes here"`
- will ask where you want to save the new keys. You don't want this to be in the default location because it will overwrite your existing keys. Instead you need an ansible specific key directory. Something like: `/home/username/.ssh/ansible` (or whatever)
- You’ll be asked to enter a passphrase for this key, ignore this and press enter
- copy key to remote server: `ssh-copy-id -i ~/.ssh/ansible.pub 10.0.0.25` (use your server IP here)
- you will be asked for your passphrase. This is not a new passphrase for the new key, this is your old, existing passphrase for your old existing key which will facilitate copying to the remote server
- press enter 
- test connection to remote server: `ssh (IP address)`
- verify public key was copied to remote server (on the remote server): `ls -la .ssh` This command should show an authorized keys file (on the remote server)
-  Check the local ssh directory on the remote server: `cat .ssh/authorized_keys` this should show there is a public key stored for ssh access to the current remote server
- enter passphrase
- view ssh directory: `ls -la .ssh`
- view public key: `cat .ssh/id_ed25519.pub`
- Make sure the correct key is used for ansible connections. On the local machine (not remote): `ssh -i ~/.ssh/ansible 10.0.0.25` (remote server IP here)

### 
