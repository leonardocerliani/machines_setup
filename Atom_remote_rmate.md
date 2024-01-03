# Atom remote file editing


Atom can be installed with the following - see [here](https://snapcraft.io/install/atom/ubuntu)

```bash
sudo snap install atom --classic
```

For `rmate` follow the procedure described at the [`remote-atom` Github repo](https://github.com/randy3k/remote-atom). The cp rmate to `usr/local/bin/rmate`

```bash
wget https://raw.githubusercontent.com/aurora/rmate/master/rmate
chmod a+x rmate
sudo cp rmate /usr/local/bin/rmate
```

Since Atom is no longer maintained, plugins need to be installed manually.
One procedure is detailed [here](https://stackoverflow.com/questions/74837424/atom-certificate-has-expired).

However, this procedure didn't work in my case (Ubuntu 22.04). Instead, I simply needed to copy the entire `remote-atom` directory inside `~/.atom/packages`.

Now you can connect to the server fowarding the port 52968

```bash
ssh -R 52698:localhost:52698 username@remote.server.com
```

Then open Atom >> Packages >> Remote Atom >> Start Server

Finally, on the server, issue `rmate [file_2_edit]` and see it appearing in Atom
