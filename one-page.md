---
# Page settings
layout: default-nonav
keywords:
comments: false

# Hero section
title: One Page Fast Guide
description: Quick 1 Page MN Setup Instructions


# Micro navigation
micro_nav: 

# Page navigation
page_nav:
    prev:
        content: Home
        url: '/'
    next:
        content: Next Steps
        url: '/next-steps'

# disqus
comments: true
---

<p>&nbsp;</p>

<div class="callout callout--info">
    <p>
    <strong>MN Hosting Instructions <i>ONLY</i> for Ubuntu 16.0.4 MN hosting.</strong>
    Although some MN users have had success using other Linux distros/versions (e.g. Debian, Ubuntu 18) and even Windows, no instructions are given here for those operating systems.
    </p> 
</div>


---
<br/>

<div class="callout callout--info">
    <p>
    Going through this guide for the first time should take approximately 30 minutes to a full hour. This isn't meant to be a quick and dirty guide, as we will cover some important information along the way. If you are setting up another Masternode, you can simply follow the steps quickly and use the copy features for the command lines. A short 1 page quick and dirty guide will be coming soon.
    </p> 
</div>

# How to Use this Guide

Hosting your own Masternode (MN) can be one of the most rewarding experiences for those wanting to invest and grow their investment in $Pac. At the same time, MN hosting *may* be too complicated for some. I've tried to simplify these instructions as much as possible (and heavily borrowing from other guides), however if any of these instructions seem too daunting or intimidating, there are alternatives to hosting a $Pac MN yourself. 


Shared Masternode services allow investors without the full amount of collateralization needed for an MN (500K $Pac) to pool resources with other investors into a shared MN. There are a few shared MN services that exist. One that I would recommend is [Pacnode.net](https://pacnode.net/){:target="_blank"}. 


<a href="https://pacnode.net/" target="_blank"><img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacnode.png" style="margin-left: auto;margin-right: auto;width: 30%;"/></a>



[Pacnode](https://pacnode.net/){:target="_blank"} has one of the best interfaces and services for the casual investor and is constantly innovating new features into their service. These shared MN services charge a percentage fee for hosting and may be a better option for you. I **DO NOT HAVE ANY** vested interest in Pacnode, I just know a lot of investors are happy with the service.


Now that you are ready to jump into exciting world of Masternode hosting, here is a quick flyover of the steps we will take to set up your MN:

<b>Steps to create your Master Node</b>
1. Getting Ready
2. Configure your desktop wallet
3. Install Master Node server on your VPS
4. Start your Master Node
5. Monitor your Master Node and collect rewards

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

Before starting, let's get our favorite standby text editor ready to go. This part will save you a lot of time as you can copy/past items instead of typing them in directly. If you are on Windows, you can use the built in <strong>Notepad</strong> program. For Mac, you can use the <strong>Notes</strong> application. Here are some good alternatives that are also free for both Windows and OSX:
- [Visual Studio Code](https://code.visualstudio.com/){:target="_blank"} (used to create this site)
- [Atom](https://atom.io/){:target="_blank"}
- [Sublime](https://www.sublimetext.com/){:target="_blank"}

<br/>

# Basic $Pac Network Overview



<div class="callout callout--info">
    <p>
    There are 2 separate parts to a Masternode setup: Your <strong>Cold aka Desktop Wallet</strong> and your <strong>Hot aka MN server wallet. </strong>In this guide, we will be referring to cold and desktop interchangeably, as well as hot and MN/server as show below
    </p> 
</div>


For the purposes of this guide, there are 3 main components of the $Pac Masternode Network that are important (this *is not* meant to be a detailed explanation of how the network is constructed, you can google that).

1. Desktop with $Paccoin Core Desktop Wallet installed, aka cold wallet: This is the main $Pac wallet, where you can send and receive $Pac as well as **remotely** start your Masternode and broadcast its address and collateral id onto the $Pac Network.

2. VPS with $Pac Masternode software and Sentinel installed, aka hot wallet: This is where the $Pac MN process `paccoind` runs participating in the second tier of the $Pac network, supporting instant sends (instantPac). It is also where the `sentinel` program resides, which periodically broadcasts your MN presence to other Masternodes.

3. $Pac Network: This is where the core nodes and all of the other $Pac Masternodes reside. Both your desktop as well as your Masternode connect to the network to syncrhonize their copies of the $Pac blockchain and, importantly, this is where your Masternode gets validated. The network of $Pac MNs also decides which MN will receive the next block reward.


<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacdiagram.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

# Communicating with your hosted MN Server



## SSH Client
SSH is a secure network protocol for communicating with your remote Masternode server. If you are using Mac OSX as your desktop wallet, then you already have an ssh client installed via the terminal application. If you are on Windows, you can download the free and opensource [Putty](https://www.putty.org/){:target="_blank"} program. Another good Windows ssh client is [Bitvise](https://www.bitvise.com/ssh-client){:target:"_blank"} (thanks Artsy!). Once downloaded and installed, proceed to the next step.

## Generating SSH Keys

Configuring SSH keys for your local desktop machine will save time as you can export your public key to your MN server and only remember a single password instead of having to type in the password to your remote server every time you login. 
    

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

You've now made sure to have both a text editor, ssh environment, and (optionally) ssh key pair generated. 
We're now ready to [Configure the desktop cold wallet]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop) which will be used to both collateralize and remote start our Masternode server.

<br/>

---


_If you find yourself stuck_, the $Pac community is always there to help. You can find the support channel on the [$Pac Official Discord](http://discord.me/pac){:target="_blank"}. 

<br/>
<br/>