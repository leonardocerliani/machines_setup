# How to create a directory with shared rwx for the users in a group

```bash
# create group
sudo groupadd GUTS

# create user
sudo useradd -m leonardo
sudo passwd leonardo
sudo usermod -aG sudo leonardo
sudo chsh -s /bin/bash leonardo

# act as that user
su - leonardo

# add to group
sudo usermod -aG GUTS leonardo
getent group GUTS

# To create a shared environment
# Make sure you have the following in the .bashrc
umask 002

# When creating a new dir, give the following permissions to the group
mkdir shared_dir                     # create the directory
sudo chown :GUTS shared_dir          # set group ownership to GUTS
sudo chmod 2775 shared_dir           # set permissions: rwxrwsr-x and setgid bit

# Apply these changes to a previously existing dir
sudo chown -R :GUTS private_dir
chmod -R g+rw private_dir
find private_dir -type d -exec chmod 2775 {} +
```


