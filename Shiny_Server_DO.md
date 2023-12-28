

Most of this comes from [this guide](https://www.digitalocean.com/community/tutorials/how-to-set-up-shiny-server-on-ubuntu-20-04)


## Set up the Ubuntu 20.04 server

```bash
# Create a droplet with Ubuntu 20.04 using pw

adduser leonardo
usermod -aG sudo leonardo

# Set up basic firewall

ufw app list
ufw allow OpenSSH
ufw enable
ufw status
```

## Install R

```bash
# add the GPG key

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9

# add the repository

sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/``'

sudo apt update
sudo apt install r-base

# Install pkgs as root

sudo -i R
install.packages('dplyr')
```


## Install nginx to open ports 80 and 443

```bash
sudo apt update
sudo apt install nginx
sudo ufw app list
sudo ufw allow 'Nginx Full``'
sudo ufw status
systemctl status nginx

# Setup server blocks
sudo mkdir -p /var/www/psaraki.xyz/html
sudo chown -R $USER:$USER /var/www/psaraki.xyz/html
sudo chmod -R 755 /var/www/psaraki.xyz
```
    
## Create a simple web page and serve it (see below for the content)
`sudo nano /var/www/psaraki.xyz/html/index.html`


```html
<html>
    <head>
        <title>Welcome to your_domain!</title>
    </head>
    <body>
        <h1>Success!  The your_domain server block is working!</h1>
    </body>
</html>

``` 

## Create the directives
`sudo nano /etc/nginx/sites-available/psaraki.xyz`

```bash
server {
        listen 80;
        listen [::]:80;

        root /var/www/psaraki.xyz/html;
        index index.html index.htm index.nginx-debian.html;

        server_name psaraki.xyz www.psaraki.xyz;

        location / {
                try_files $uri $uri/ =404;
        }
}
```


## Final adjustments and testing nginx
```bash
# Create a link to `sites-enabled`
sudo ln -s /etc/nginx/sites-available/psaraki.xyz /etc/nginx/sites-enabled/

# Adjust hash bucket memory
sudo nano /etc/nginx/nginx.conf

# Remove the `#` in front of `server_names_hash_bucket_size`

# Test and restart nginx
sudo nginx -t
sudo systemctl restart nginx
```

#EOF