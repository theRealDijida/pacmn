---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Install Your Masternode Server
description: 


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Configure Desktop Wallet
        url: '/configure-desktop'
    next:
        content: Start Your Masternode
        url: '/start-mn'

# disqus
comments: true
---

<p>&nbsp;</p>
We are now ready to install the Masternode server on your remote vps. 
A quick reminder of where we are below:

<b>Steps to create your Master Node</b>

- [x] &nbsp; ~~1. Getting Ready~~
- [x] &nbsp; ~~2. Configure your desktop wallet~~
- [ ] &nbsp; <mark>3. Install Master Node server on your VPS</mark>
- [ ] &nbsp; 4. Start your Master Node
- [ ] &nbsp; 5. Monitor your Master Node and collect rewards


# Choose a VPS Host Provider

Your VPS (Virtual Private Server) hosts the $Pac Masternode software and contains your hot wallet. While your cold aka desktop wallet can be shut down and offline, your hot wallet aka MN server must be connected to the internet and always running the $Pac Masternode server software. 

There are many vps hosts out there. This guide will walk you through setting up your $Pac Masternode on a popular hosting provider: Vultr. 


If you want to use my referral link, you can click here: [https://www.vultr.com/?ref=7481728](https://www.vultr.com/?ref=7481728) or the image belwo (full disclosure, I get credits on hosting if you use this). 

<a href="https://www.vultr.com/?ref=7481728"><img src="https://www.vultr.com/media/banner_1.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"></a>

<br/>

If not, _no biggie_ (I know, I even feel like taking a shower after putting up that referral link), just go directly here [Vultr.com](https://www.vultr.com). If you are setting up your Masternode on another VPS host, follow the basic steps set up here with those for your specific host. The general process should be the same except for Vultr specifics. Once you are done registering and setting up your account information and billing, proceed ahead.

<br/>
<div class="callout callout--warning">
    <p>
    When setting up your vps hosting account, please make your passwords sufficiently secure.
    </p>
</div>


<br/>


# Create Your VPS Instance

## Create New VPS


Once you login into your vultr dashboard, click on the "Server" tab to the left hand side of the screen. Refer to the screen shot below and follow the steps:

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>
- 1\. Click on the blue circle to create your virtual private server to host your $Pac Masternode.


## Choose Hosting Location

Vultr has a lot of datacenters you can choose from to host your vps instance. Refer to the screen shot below and follow the next step: 

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-location.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

<div class="callout callout--info">
    <p>
    Although you can pick whichever you want, I personally recommend choosing a US based server. Why? As of this writing, almost 45% of the Masternodes currently on the network reside in US based datacenters. MNs, especially when first starting, need to constantly synch and communicate with each other. If you choose a datacenter location that is far away from a community of MNs then it will take a tiny bit longer for each communication. 
    </p>
    <p>
    This is a really small amount, so it may not bother you. You can see the current Masternode node at the <a href="http://explorer.paccoin.net/map" target="_blank">$Pac Explorer site</a>
    </p> 
</div>


- 2\. Choose any server location, as seen in the screen shot below. Just please don't pick Miami. I don't know why, but I've had several users with issues in that datacenter location with vultr. I myself have had issues there as well, with random reboots. Any other location should be fine. 


Once you've selected a location, proceed ahead.

## Choose Server Type and Size

In this step, you will select the operating system for your Masternode as well as the virtual server size. The supported and recommended operating system is **Ubuntu 16.04** and the recommended vps size is the **$5/mo** plan on vultr which will give you 1Gb of RAM for the vps. 


I know, I know, lots of users are hosting multi-coins on their vps, maybe even using Debian, or installing the MN onto a raspberry Pi. More power to you if you can do it. This configuration: **Ubuntu 16.04 and 1Gb RAM ($5/mo plan)** is the recommended configuration and will end up giving you the smoothest Masternode experience.

From the screen shot below:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-type-size.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

- 3\. Select **Ubuntu 16.04**
- 4\. Select the **$5/mo** plan (25GB SSD, 1 CPU, 1024MB Memory)

## Configure SSH

Recall from the First Steps section, where we [generated ssh keys]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/first-steps#generating-ssh-keys) for communicating securely with our Masternode server. Have your text editor ready where you had previously copied your public ssh key and follow the steps below, referencing the screen shots:

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-ssh-host.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

- 5\. Click "Add New" button under the "SSH Keys" section which will lead you to the screen below:

<br/>



<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-ssh-add.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

- 6\. Enter a name in this field, whatever you want.

- 7\. From your text editor, where you copy/pasted your public ssh keys, copy the complete string and paste it into this field.

- 8\. Click the "Add SSH Key" button.

You'll be directed to the previous screen. We are nearly done setting up the vps.

## Set Hostname and Deploy

Setting a unique hostname for your Masternode vps can be quite handy, especially if you plan on setting up more than one Masternode. I recommend setting a name for your vps host which is the same as the _Unique MN Receive Address_ you configured in [step 2 of Configure Your Desktop Wallet/Create Unique MN Wallet Address]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop/#create-unique-mn-wallet-address). This will help you keep track of your Masternodes, especially when you are running multiple MNs.


Refer to the screen shot below and follow the steps:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-deploy.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

- 9\. Enter a hostname for your vps, e.g. "MyMN1".

- 10\. Click the "Deploy Now" button.

You will be sent back to the Servers tab of your Vultr dashboard with your newly created vps instance and see something like the screen shot below:

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/v-servers-info.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>


- 11\. Click the "copy" icon next to your vps "IP Address" and paste it into your text editor. We will need Your new VPS IP Address in the section, where we install the $Pac Masternode software.

<div class="callout callout--info">
    <p>
    Make sure to double check all of your information (see screen shot). You'll notice that following the naming scheme as explained in this guide will make your life much easier, especially as you invest in more $Pac masternodes. Also, in the sceen shot, in the upper right, you'll see some icons that may come into use at a later point in time to stop and restart your vps.
    </p> 
</div>


In the next section, we'll connect from our desktop to our remote vps and install the $Pac Masternode software.


# Install $Pac Masternode Software

## Login via SSH to your Remote VPS

From your desktop, we'll first set up a secure remote ssh session to the vps you just created. Follow the instructions below for your particular operating system. You will need the IP Address of the vps you just created.

### Windows

You can find instructions on connecting to your vps via putty using the link below. Go to the section labeled "Log in to PuTTY with the private key". These instructions can be found here:

[https://support.rackspace.com/how-to/logging-in-with-an-ssh-private-key-on-windows/](https://support.rackspace.com/how-to/logging-in-with-an-ssh-private-key-on-windows/){:target="_blank"}.

Once you've established your ssh session to your vps, proceed to the next step [Install $Pac Masternode Script](#install-$pac-masternode-script).

### Mac

Open Launchpad and search for the application "Terminal". A basic terminal shell window will open. You may want to expand the size so it is easier to see the output. 

<br/>


<div class="example" >Type the following into your terminal shell
</div>
```
ssh root@YOUR_IP_ADDRESS
```


- 1\. In your terminal shell at the prompt, type the line above, replacing 'YOUR_IP_ADDRESS' with the ip address of your vps, for example,if your vps IP Address is 127.0.0.1, you would type 'ssh root@127.0.0.1'. See the sceenshot below as an example:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/ssh-login.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

- 2\. Press Enter.
- 3\. You will be prompted for the passphrase you entered when generating your key pair. Type in your passphrase and hit enter.


## Set Language Locale

If you are using a different language on your desktop machine than English, you will need to execute the following steps. This is necessary because part of the $Pac Masternode install process involves setting up a support process called Sentinel. This process will fail if your vps is set to a non-english locale. When you connect to your vps remotely via ssh (as in the prior step), your ssh client will automatically set your desktop locale onto the ssh session of your remote vps. This means that if you are in Paris, *even though* your vps location is in New York, your ssh session will be set to the French locale and your $Pac MN install will fail.

Copy and paste the following into your ssh client and press enter:

<div class="example" >Set English Locale
</div>
```bash
export LC_ALL="en_US.UTF-8"
```


## Install $Pac Masternode Script

Next we will install the $Pac Masternode software from the offical $Pac Github Repository. 

Copy and Paste the following into your terminal. This will pull down the installer script for the $Pac MN process (paccoind) as well as the Sentinel process (more on this later). Clicking the copy icon will automatically copy this onto your clipboard.

**Note** If you can't see all of the text above, scroll horizontally.


<div class="example" >$Pac MN Installer (click copy icon)
</div>
```bash
wget https://raw.githubusercontent.com/PACCommunity/PAC/master/pacmn.sh && chmod +x pacmn.sh && ./pacmn.sh
```

If you used the copy icon, you can simply paste using - Windows: Ctrl+V or Mac: Command+V into your ssh client.
Otherwise press enter to continue.

You will be prompted for 2 pieces of information: 1) Your VPS IP Address from the previous step, and 2) Your Masternode Private Key.
Both of these should be in your text editor from previous steps. Enter the information when prompted.

<br/>

<div class="callout callout--warning">
    <p>
    You will see a lot of information scrolling in the window as the installer progresses. 
    <strong>If you see ANY ERRORS</strong> do not continue with the following steps, just bookmark your progress here, and refer to the trouble shooting section of this guide. Most of what I've seen are errors in the sentinel install at the tail end of the process.
    </p> 
</div>

## Install $Pac MN Service



# Configure Desktop Masternode Config File

# Remote Start Masternode


## Next Step: Start Your Masternode

Now that we've installed our Masternode software, our next step is to [Start the Masternode](/start-mn) so that it is visible on the network.



