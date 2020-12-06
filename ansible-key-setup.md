### Ansible Key Setup
- create ssh key dedicated to this repo: `ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "comment goes here"`
- will ask where you want to save the new keys. You don't want this to be in the default location because it will overwrite your existing keys. Instead you need an ansible specific key directory. Something like: `/home/username/.ssh/ansible` (or whatever)
- You’ll be asked to enter a passphrase for this key, ignore this and press enter
- copy key to remote server: `ssh-copy-id -i ~/.ssh/ansible.pub 10.0.0.25` (use your server IP here)
- you will be asked for your passphrase. This is not a new passphrase for the new key, this is your old, existing passphrase for your old existing key which will facilitate copying to the remote server
- press enter 
- test connection to remote server: `ssh (IP address)`
- verify public key was copied to remote server (on the remote server): `ls -la .ssh` This command should show an authorized keys file (on the remote server)
- view the authorized keys file: `cat .ssh/authorized_keys`. this should show that both keys are stored for ssh access to the current remote server
- Test the connection using the correct (ansible) key: `ssh -i /.ssh/ansible 10.0.0.25` (use the remote server IP here)
- 
### 
