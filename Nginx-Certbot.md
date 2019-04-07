---
title: Configure Nginx and TLS Certifications on Your Server
layout: topic
categories: guide
---

Now that you have a domain and a server, you need to configure 
the server to serve content to your domain.

The two most common web server software suites are 
[`nginx`](https://nginx.org/) and [`apache`](https://www.apache.org/). 
This wiki page will cover web server configuration with `nginx` 
because it is easier to configure for first-time users. The wiki page 
assumes that the machine used to serve content is a Digital Ocean 
droplet, but the specific steps won't differ widely between services.

## Step 1: Install `nginx`

Installation is relatively easy.
- ssh into your droplet.
- To confirm that the software is not currently installed, run the 
  following command:<br>
  ```
  $ which nginx
  $
  ```
  <br>
  If you see no executable path before the prompt reappears, then you 
  will need to install `nginx`.
- Install `nginx` with the following command:<br>
  ```
  $ sudo apt-get install nginx
  ```
  <br>
  When prompted with `Do you want to continue? [Y/n]`, type yes and 
  press return.
- To confirm that `nginx` was installed, rerun `which nginx`.
  You should now see a path to the executable in the console.

## Step 2: Get Your Website Code onto the Server

Assuming that your code is in a `git` repository, clone the repository 
onto your machine.

In our example, we will be serving 
[this GitHub repository](https://github.com/UWB-ACM/website-example-2) 
at [phry.me](http://phry.me).

To clone the repository, run the following commands and replace the 
GitHub URL with the URL to your own repository.

```
$ cd /var/www
$ git clone https://www.github.com/UWB-ACM/website-example-2.git
$ cd website-example-2
$ pwd
/var/www/website-example-2
```

Note: the output for the `pwd` command will be important for the 
next step.

## Step 3: Set Up Configuration for `nginx`

Now that you have the source code for your website on your machine, 
you need to point `nginx` to the directory of the source code and 
ensure that the content gets served on your domain.

The configuration file your your site will be located under `/etc/nginx/sites-available`. On a fresh installation of `nginx`, a 
site configuration file called `default` is provided as an example.

Run the following commands and replace `phry.me` with the domain name 
you chose. _Note: this isn't a strict requirement, but is a common 
naming convention. It is recommended to use naming conventions._

```
$ cd /etc/nginx/sites-available
$ ls
default
```

Now, in your preferred text editor, create a file named `phry.me` 
(or whatever your domain name is). Add the following text to the 
file:

```
server {
    # replace the filepath with the output from the pwd command from step 2
    root /var/www/website-example-2;
    # the file name should be the desired homepage file for your website located in the directory named in the previous line
    index index.html;       
    # this line is for the domain name you chose
    # make sure the domain name matches the one you bought!
    server_name phry.me lol.phry.me;

    # these lines will help protect users from accessing raw files in your repository folder
    location / {
        try_files $uri $uri/ =404;
    }
}
```

Save and close the configuration file.

Next, we need to set up a symbolic link to this raw file in the 
`/etc/nginx/sites-enabled` directory, so that `nginx` serves the 
content.

Run these commands:

```
$ cd /etc/nginx/sites-enabled
$ ln -s ../sites-available/phry.me .
```

_Note: don't forget to replace `phry.me` with the filename you chose 
when creating the configuration file in `/etc/nginx/sites-available`._

Now, we need to restart the `nginx` process on the machine.

```
$ systemctl restart nginx.service
```

If you do not see an error code on the last command, then `nginx` 
successfully restarted and should be serving the content from the 
cloned repository.

_If you do see an error message, seek help from a hackathon mentor!_

## Step 4: Enable HTTPS Traffic to Your Domain with CertBot

[CertBot](https://certbot.eff.org/) is a tool created by the 
[Electronic Frontier Foundation](https://www.eff.org/) to deploy 
SSL/TLS encryption certificates on your machine so that your web 
traffic can be served over HTTPS. This helps ensure your website and 
the user accessing your site remain secure.

To get started, install the necessary packages by running these 
commands:

```
$ sudo apt-get update && apt-get upgrade
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install python-certbot-nginx
```

Now that the CertBot client is installed, generate a certificate for 
your site by running the following command:

```
$ certbot run
```

You will be prompted for the following information:
- **Enter an email address:** you will receive emails at this address 
  when the certification is due for renewal, or if any important 
  security notices need to be shared with you.
- **Agree to Terms of Service for Let's Encrypt:** Enter `A` to 
  continue.
- **Share contact information with the EFF:** this is completely 
  optional, but EFF is a great organization and it's up to you as to 
  whether you want to receive correspondence from them.
- **Choose domains to activate HTTPS for:** CertBot will 
  automatically detect domains that `nginx` is serving content for. 
  It is advisable to add HTTPS certificates for all domains.
  You can:
  - Select multiple domains individually by numbered listings 
    on the console prompt
  - Leave the input blank to add certificates for all domains listed
  - Enter `c` to cancel the certification process
- **Choose whether to redirect HTTP traffic to HTTPS:** selecting 
  option 2 will redirect all HTTP traffic to HTTPS; this is the best 
  option for security. It is recommended to select option 2 unless 
  your project has a very specific use case for HTTP traffic.

That's it! You should be able to test your new website from any 
computer and any browser and see it live. For example, take a look 
at [lol.phry.me](https://lol.phry.me/).
