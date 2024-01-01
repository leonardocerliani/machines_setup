# Editing and running on remote machines

## SSH with public key
Generic procedure to connect to the remote server without password. 

- Check that `~/.ssh` exists both in the local machine and on the server, otherwise create it 
- Check if `~/.ssh/id_rsa.pub` - as well as the private key - exists, otherwise create it with `ssh-keygen`. Other options are available, e.g. `ssh-keygen -t rsa -b 4096 -C "pippo@remote.server.com"`
- Copy the public key in the `authorized_keys` on the server with `ssh-copy-id pippo@remote.server.com`
- If everything went well, you should be able to `ssh pippo@remote.server.com` without pw

---

## Colab using remote python kernel
The main idea is to fw a local port on the remote server, so that the messages to the remote server on the specified port will be fw'ed to the (usually same) local port

Then we launch a jupyter nb session on the remote machine, and finally we connect Colab to the remote server through the specified https token.

Importantly, we usually want to use a specific conda/virtual environment, therefore we should first activate it on the _remote_ server before launching the jupyter notebook server.

---

On the local machine, connect to the server with port forwarding
```bash
ssh -L 8888:localhost:8888 pippo@remote.server.org
```

On the server, create (if necessary) a new virtual environment, activate it and install jupyter and other desired packages.

Then start the jupyter notebook server - see also [here](https://research.google.com/colaboratory/local-runtimes.html)

```bash
python -m venv colab-env
source colab-env/bin/activate
pip install jupyter numpy

jupyter notebook \
    --NotebookApp.allow_origin='https://colab.research.google.com' \
    --port=8888 \
    --NotebookApp.port_retries=0
```

When launching the jupyter notebook server, a link will be displayed at the bottom, such as:

```bash
http://localhost:8888/tree?token=45x3cbedd647d780e1564892fa7343262fg79d761dfd2a83a0
```

On the local machine, open a Colab >> Connect to a _local_ runtime, and paste the link above.

Now your Colab notebook is connected to the remote kernel, and can read/write files on the remote server. To test this, try e.g. `!PWD` or `!echo $VIRTUAL_ENV` inside Colab.




