---
title: Create a Web Server on Digital Ocean
layout: topic
categories: guide
---

In order to get your website deployed, you will need to create and configure a machine to do that. This page has all the information you need to create and configure a Digital Ocean droplet to host your website.
_Note:_ you are welcome to use any cloud provider you are comfortable with. Setting up a machine on Digital Ocean is fast and easy, but you can use AWS, Azure, or any other service provider you prefer. Please note that the technical advisors at the hackathon may not be able to help you troubleshoot account issues for the provider you choose to go with.

## Step 0: Create an Account on Digital Ocean

- Create an account on [Digital Ocean](https://cloud.digitalocean.com/registrations/new). You will need four pieces of information to complete your account setup:
  - Your name (individual or team name)
  - A valid email address
  - A password for your account
  - A credit or debit card to link to the account
- You will receive a confirmation email after registering; click the confirmation link to finalize account creation.
- After clicking the confirmation link, you will be taken to a billing page. Please have a credit or debit card ready to link to your new account. _Note: this is a common requirement for all service providers; note that you can suspend services to limit your charges at any time._
- Next, you will be prompted to create a project. 
  - Make sure you give your project a sweet name! 
  - For the **What is your project for?** question, you can select whichever category you prefer. We recommend _Class project / Educational purposes_, but you may prefer _Web Application_, _Website or blog_, _Service or API_, or _Other_.
  - For the deployment tools section of this page, you can select anything you know you will be using; when in doubt, skip this step.
  - At the bottom of the page, change the slider to reflect how many people are on your team.

## Step 1: Create Your Digital Ocean Droplet

A **Droplet** is a fancy term Digital Ocean (DO) came up with; fundamentally, it is a remote virtual machine that they provide hardware and infrastructure for. A droplet that you create can be used to deploy websites, run bots, build and run large projects, or anything else you want. 

Digital Ocean droplets are scalable -- if or when you need more (or less) computational resources, you can change the specifications of your droplet in your DO account management page.

To create your first droplet, follow these steps:

- Log into your brand-new DO account and navigate to your project dashboard. Your dashboard should look something like this:
- Scroll down a little and click "Create Droplet".
- The next page will have settings for your new droplet.
  - **Choose an operating system.** The DO menu defaults to Ubuntu, and we recommend using Ubuntu. You are welcome to use any distribution you prefer, but Ubuntu is easy (and the technical advisors at the hackathon will have an easier time helping you with configuration if you need help).
  - **Choose a pricing plan.** The DO menu defaults to a pricing plan of $40.00 per month. We recommend picking a more affordable plan. Click the _left arrow_ to see cheaper plans. The $5.00 per month plan features 25GB of disk storage and 1GB of RAM; this will most likely be more than enough for your project.
  - **Choose extra options.** DO offers backups for your machine at an extra cost; feel free to ignore this option (especially if you are using version control on your project). Likewise, feel free to ignore the "Add block storage" option unless you feel you will need more disk space for your project.
  - **Choose a datacenter region.** Feel free to choose a region that speaks to you personally. Leaving the default setting as-is should be perfectly fine.
  - **Add SSH keys.** Skip this step for now; SSH keys will be discussed later in this tutorial.
  - **Final steps.** 
    - For the _How many Droplets?_ question, leave the existing selection (1 Droplet) as is unless you explicitly need multiple machines.
    - For the _Choose a hostname_ section, pick a sweet computer name! You can leave it on the default setting, but who wants a computer name like `ubuntu-s-1vcpu-1gb-nyc1-01`?
    - For the _Select project_ section, make sure your project name is selected.
  - Click _Create_.

When the droplet has been created, your Project Dashboard will show the droplet with the hostname you picked and the droplet's IP address.

**Further Reading:** Digital Ocean has good instructions [here](https://www.digitalocean.com/docs/droplets/how-to/create/).

## Step 2: Log Into Your Droplet

After the droplet is created, you will receive an email with credentials for your droplet's `root` account. The email will look something like this:

On first login, you will be required to change the password for `root`. Make it something memorable!

To log in, SSH into the box using the credentials from your email. An example of the process is provided below.

```bash
me@laptop: ~ $ ssh root@142.93.7.108
The authenticity of host '142.93.7.108 (142.93.7.108)' can't be established.
ECDSA key fingerprint is SHA256:vKp9jX5M51C66KvzURZJ2HCcRuQlQ0PJEaX5spfPKkk.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '142.93.7.108' (ECDSA) to the list of known hosts.
root@142.93.7.108's password: 
You are required to change your password immediately (root enforced)
Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-45-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Tue Mar 12 02:55:29 UTC 2019

  System load:  0.08              Processes:           79
  Usage of /:   3.9% of 24.06GB   Users logged in:     0
  Memory usage: 11%               IP address for eth0: 142.93.7.108
  Swap usage:   0%

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

Changing password for root.
(current) UNIX password: [REDACTED]
Enter new UNIX password: [REDACTED]
Retype new UNIX password: [REDACTED]
root@hacking-the-planet: ~ # echo "hello world"
hello world
```

You are now all set to use your droplet!

## Step 3 (Optional): Set up Non-Root Account(s) For Your Teammates

This is ***strongly*** recommended for security and traceability of user access. A brief summary of the required steps are as follows:

1. SSH into your new droplet's root account: `ssh root@DROPLET_IP`.
2. Create a new user with the command `adduser *username*`, where `*username*` is replaced with the username of your choice.
3. When prompted, choose a password for the new user.
4. When prompted, you can fill in the user's contact information. For ease of use, you can leave the fields as-is.
5. If your new user needs `sudo` privileges (which is likely), you can grant sudo privileges to the new user with the following command: `usermod -aG *username*`

**Further Reading:** Detailed instructions for creating new users are [here](https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-an-ubuntu-14-04-vps). Detailed instructions for granting sudo access to new users are [here](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart).

## Step 4 (Optional): Add SSH Keys for Team Access

This is ***strongly*** recommended for security and traceability of user access, ***especially if you do not create individual accounts for your teammates***. This step will give your teammates access to the droplet without having to distribute the root password to all teammates.

1. Have your teammates generate an SSH key for the droplet. Detailed instructions on how to do this are described [here](https://www.ssh.com/ssh/keygen/). 
    <br>It is recommended to generate a key using `rsa` or `ed25519` algorithms, and giving the keyfile a memorable name (how about `hackathon`?). Note that when specifying a new key name, you need to provide the absolute path to the `~/.ssh` folder, and further specify the filename with no extension.
2. Obtain the newly created ***public*** key file from your teammate. There are two files that get generated with the `ssh-keygen` command; the ***public*** key file is appropriately named with the `.pub` extension. _Friendly Reminder: distributing a **private** key exposes your droplet and your teammate to security vulnerabilities._
3. Add the public key file to your droplet with the following commands: 
    <br>`scp ~/teammate_key.pub root@DROPLET_IP:~`
    <br>`ssh root@DROPLET_IP`
    <br>`mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys`
    <br>`cat ~/teammate_key.pub >> ~/.ssh/authorized_keys`
4. Ask your teammate to log into the droplet to confirm their access works.

**Further Reading:** Detailed instructions for adding your keys to the droplet are available [here](https://kb.iu.edu/d/aews), along with instructions for PuTTY/Windows.
