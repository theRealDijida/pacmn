---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: First Steps
description: Step by Step instructions for setting up your first $Pac Master Node


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Home
        url: '/'
    next:
        content: Configure Desktop Wallet
        url: '/configure-desktop'

# disqus
comments: true
---

<p>&nbsp;</p>

<div class="callout callout--info">
    <p>
    <strong>These Instructions Are <i>ONLY</i> for Ubuntu 16.0.4 MN hosting.</strong>
    Although some masternode users have successfully used other Linux distros/versions (e.g. Debian, Ubuntu 18) and even Windows, this guide is only meant to work with Ubuntu 16.
    </p> 
</div>


---
<br/>

<div class="callout callout--info">
    <p>
    Going through this guide for the first time should take around 30 minutes to an hour. If you have already set up a masternode, you can use the quick <a href="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/one-page">One Page Guide</a>.
    </p> 
</div>

# How to Use this Guide

Hosting your own Masternode (MN) can be a rewarding experience for those wanting to grow their investment in $Pac. At the same time, MN hosting *may* be too complicated for some. This guide has been simplified as much as possible, but if it seems too daunting or intimidating, there are alternatives to hosting your own $Pac MN. 


Shared Masternode services allow investors without the full amount of collateral needed for an MN (500K $Pac) to pool resources with other investors into a shared MN. There are a few shared MN services out there, and one that I would recommend is [Pacnode.net](https://pacnode.net/){:target="_blank"}. 


<a href="https://pacnode.net/" target="_blank"><img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacnode.png" style="margin-left: auto;margin-right: auto;width: 30%;"/></a>



[Pacnode](https://pacnode.net/){:target="_blank"} has one of the best interfaces and services for the casual investor and is constantly innovating new features into their service. These shared MN services charge a percentage fee for hosting and may be a better option for you. I **DO NOT HAVE ANY** vested interest in Pacnode, I just know a lot of investors are happy with the service.


Now that you're ready to jump into exciting world of Masternode hosting, here is a quick overview:

<b>Steps to create your Master Node</b>
1. Getting Ready
2. Configure your Desktop Wallet
3. Install Masternode server on your VPS
4. Start your Masternode
5. Monitor your Masternode and collect rewards

-----

As we go along, you will notice some guideposts along the way including:

<b>Steps that are important to follow in order:</b>

- 1\. Step 1
- 2\. Step 2

<br/>
<b>Call outs for typing in commands:</b>
<div class="example" >Instruction Step
</div>
```bash
type this exact command or use copy to clipboard
icon directly below
```
Click the <i class="fas fa-copy"></i> copy button above (directly below the command) to copy to your clipboard for easy copy/paste into your ssh program (see below):

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/click.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>


This will also include the new line character for convenience (so you don't have to press enter after pasting using this method).


To paste after copying using for Windows: Ctrl+V and for Mac: Command+V.



<br/>
<b>Warnings and Gotchas:</b> are displayed in yellow callouts as shown below.
<div class="callout callout--warning">
    <p><strong>Pay extra attention!</strong> </p>
</div>

<br/>

# Text Editor

Before starting,  get your favorite standby text editor ready to go. This part will save you a lot of time as you can copy/paste instead of typing commands in directly. If you are on Windows, you can use the built in <strong>Notepad</strong> program. For Mac, you can use the <strong>Notes</strong> application. Some good alternatives that are free for both Windows and OSX include:
- [Visual Studio Code](https://code.visualstudio.com/){:target="_blank"} (used to create this site)
- [Atom](https://atom.io/){:target="_blank"}
- [Sublime](https://www.sublimetext.com/){:target="_blank"}

<br/>

# Basic $Pac Network Overview



<div class="callout callout--info">
    <p>
    There are 2 separate parts to a Masternode setup: Your <strong>Cold Wallet (installed on desktop)</strong> and your <strong>Hot Wallet (installed on server). </strong>In this guide, we will be using "cold" and "desktop" interchangeably, as well as "hot" and "MN/server" as shown below.
    </p> 
</div>


For the purposes of this guide, there are 3 main components of the $PAC Masternode Network that are important (this *is not* meant to be an exhaustive explanation of how the network is constructed. If you need more information, you can Google it).

1. Desktop with $PAC Wallet installed (also known as the cold wallet): This is the main $PAC wallet, where you can send and receive $Pac, where the 500K $PAC collateral will be stored, as well as **remotely** starting your Masternode and broadcasting its address and collateral id onto the $PAC Network.

2. VPS with $Pac Masternode software and Sentinel installed (also known as the hot wallet): This is where the $Pac MN process `paccoind` participates in the second tier of the $Pac network, supporting instant sends (instantPac). It is also where the `sentinel` program resides, which periodically broadcasts your MN presence to other Masternodes.

3. $Pac Network: This is where the core nodes and all of the other $Pac Masternodes reside. Both your desktop as well as your Masternode connect to the network to syncrhonize their copies of the $Pac blockchain and, importantly, this is where your Masternode gets validated. The network of $Pac MNs also decides which MN will receive the next block reward.


<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacdiagram.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

# Communicating with your hosted MN Server



## SSH Client
SSH is a secure network protocol for communicating with your remote Masternode server. If you are using Mac OSX as your desktop wallet, then you already have an ssh client installed via the terminal application. If you are on Windows, you can download the free and opensource [Putty](https://www.putty.org/){:target="_blank"} program. Another good Windows ssh client is [Bitvise](https://www.bitvise.com/ssh-client){:target:"_blank"} (thanks Artsy!). Once downloaded and installed, proceed to the next step.

## Generating SSH Keys

Configuring SSH keys for your local desktop machine will save time as you can export your public key to your MN server and only remember a single password instead of having to type the password to your remote server every time you login. 
    

### Mac OSX
Follow this [link](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#platform-mac){:target="_blank"} from the github help docs for instructions on generating a new ssh key pair. 

Once you've followed those steps, then:

- 1\. Execute the command below to copy your newly generated public key onto the clipboard:

<div class="example" >Copy Public SSH Key to Clipboard
</div>
```bash
pbcopy < ~/.ssh/id_rsa.pub
```
and then 

- 2\. Paste them into your text editor (Command-V).

### Windows
[Easy Instructions](https://docs.joyent.com/public-cloud/getting-started/ssh-keys/generating-an-ssh-key-manually/manually-generating-your-ssh-key-in-windows){:target="_blank"} from the Joyent docs for configuring a new ssh key pair for Putty. If you are using Bitvise, easy instructions are found [here](https://www.bitvise.com/public-keys-in-ssh){:target="_blank"}.
<br/>

Follow all of the steps including step 8. Now that your public key is copied to the clipboard, paste it into your text editor from the [previous step](#text-editor) (Ctrl+V).

<br/>


<div class="callout callout--info">
    <p>
    We'll be using the public ssh key you just generated above when we deploy our virtual private server to install the Masternode software. Be sure to follow the steps and paste the public key into your text editor to have it ready to go.
    </p> 
</div>

<br/>

# Next Step: Configure Desktop Wallet

<br/>

You now have a text editor, ssh environment, and (optionally) ssh key pair generated. 
We're ready to [Configure the desktop cold wallet]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop) which will be used to collateralize and remote start the Masternode server.

<br/>

---


_If you find yourself stuck_, the $Pac community is always there to help. You can find the support channel on the [$Pac Official Discord](http://discord.me/pac){:target="_blank"} as well as the $Pac Masternodes Group in the link below.

<br/>
<br/>
