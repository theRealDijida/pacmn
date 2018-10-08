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
        content: First Steps
        url: '/first-steps'
    next:
        content: Monitor Your Masternode
        url: '/monitor-mn'

# disqus
comments: true
---

<p>&nbsp;</p>



<div class="callout callout--info">
    <p>
    This is a quick and dirty cheat sheet guide meant for those already familiar with Masternode setup, or if you already have a $Pac Masternode and just want to get it done quickly. It assumes you already know the basics of setting up your ssh keys and navigating the $Pac Desktop wallet
    </p> 
</div>

<br/>

- 1\. Enable Masternode Tab in your Desktop Wallet: Tools -> Options/Preferences -> Show Masternode Tab. Restart Desktop Wallet.
- 2\. Generate Masternode Private Key: Tools -> Debug Console. Enter the following:


<div class="example" >Generate Masternode Private Key
</div>
```bash
masternode genkey
```


Copy the key generated into your text editor

- 3\. Collateralize Masternode: Create a unique Receive Address (e.g. "MyMN1", "MyMN2", etc), and copy this address to your standby text editor. Each MN you own needs its own **unique** address.

- 4\. Send **exactly** 500K $Pac to the address you generated above. Wait for 15 confirmations.

- 5\. Get your output: Tools -> Debug Console, type the following:


<div class="example">Display Collateral Tx Id
</div>
```bash
masternode outputs
```


You will see a line for each masternode's 500K collateral, so if this is your second MN, you will see 2 lines. Copy the **new line** to your text editor (or the single line if this is your first MN).

- 6\. Edit the output string in your standby text editor. Remove all double quotes, and make sure there is a space between the end `0` or `1`. It should look something like the following in your text editor:

```
a89rhtuyf23jd84120942acce447830aa83lkdl3k39s73m 1
```

- 7\. Create a new VPS instance and choose `Ubuntu 16.04` and the `$5/mo` plan. Set your ssh keys, set the hostname to the same name as your Receive address in step 3, e.g. "MyMN2" and deploy your instance. Select your VPS and copy its IP Address into your text editor.

- 8\. Log into your VPS instance via ssh.

- 9\. Add Swap Space

<div class="example" >Add Swap Space
</div>
```bash
sudo fallocate -l 4G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile && echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab && free -h
```

- 10\. Install $Pac Masternode Script

<div class="example" >$Pac MN Installer (click copy icon)
</div>
```bash
wget https://raw.githubusercontent.com/PACCommunity/PAC/master/pacmn.sh && chmod +x pacmn.sh && ./pacmn.sh
```

Enter your MN IP Address and Private Key when prompted.

- 11\. Install $Pac MN Service

```bash
wget https://gist.githubusercontent.com/foxrtb/b703ae761472c5599c4d83ab0d3d62ae/raw/e8913deb9e1b7cc9c649febd2942930e4f6f5127/add-systemd-from-script && chmod +x add-systemd-from-script && ./add-systemd-from-script
```

- 12\. Verify Sync, wait for `AssetID` to get to `999`

<div class="example" >$Pac SystemD Service (click copy icon)
</div>
```bash
./paccoin-cli mnsync status
```

- 13\. Edit the `masternode.conf` file on your Desktop Wallet. Use a new line with MN alias, IP Address `:7112`, Masternode Private Key, Collateral Output and Index, all separated by spaces as shown below:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/mnconf.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>

- 14\. Save the `masternode.conf` file and close your text editor. **Restart** your $Pac Desktop wallet to apply the changes.

- 15\. Click the Masternode tab, select your MN, then choose `Start Alias` button on bottom. 

- 16\. Verify the status on your VPS:

<div class="example" >Check MN Status
</div>
```bash
./paccoin-cli masternode status
```

Make sure that the status says “Masternode successfully started”.


<br/>
<br/>

Your Masternode is now up and running! The next step is to [Monitor Your Masternode]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/monitor-mn) and collect rewards.


