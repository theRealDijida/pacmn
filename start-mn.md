---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Start Your Masternode
description: 


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Install Your MN Server
        url: '/install-server'
    next:
        content: Monitor Your Masternode
        url: '/monitor-mn'

# disqus
comments: true
---

<p>&nbsp;</p>
Next we'll edit a special file on your desktop wallet named `masternode.conf` and "Start" your MN on the $Pac network. 
A quick reminder of where we are below:

<b>Steps to create your Master Node</b>

- [x] &nbsp; ~~1. Getting Ready~~
- [x] &nbsp; ~~2. Configure your desktop wallet~~
- [x] &nbsp; ~~. Install Master Node server on your VPS~~
- [ ] &nbsp; <mark>4. Start your Master Node</mark>
- [ ] &nbsp; 5. Monitor your Master Node and collect rewards


# Edit Masternode Configuration

On your cold (desktop) wallet installation, there is a special file which contains information needed to properly remote start and broadcast your new MN to the $Pac network. To access this file, from the main toolbar go to Tools -> Open Masternode Configuration File:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/tools-mnconfig.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%;"/>

This will open the file `masternode.conf` in your text editor. The first 2 lines of the file are commented out using the `#` character and show the format needed. We'll need to enter the following 4 pieces of information that you should have already copy and pasted into your standby text editor:

(1). alias - this is a unique name for your Masternode. If you followed the recommended naming convention, this is the same name found in **step 9** of [Install Server: Set Hostname and Deploy]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/install-server/#set-hostname-and-deploy).
<br/>

(2). IP:port - this is the IP Address of your Masternode VPS that you copied from **step 11** of [Install Server: Set Hostname and Deploy]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/install-server/#set-hostname-and-deploy). Your IP Address in this file needs to be appended with `:7112`
<br/>

(3). Masternode Private Key - this is the private key we generated in **step 4** of [Configure Desktop: Generate Private Key]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop/#generate-private-key).
<br/>

(4). Collateral Output and Index - this is the collateral id and index of the 500K $Pac we sent to collateralize our Masternode, properly formatted, and found from **step 5** of [Configure Desktop: Get Collateral Tx Id]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop/#get-collateral-tx-id).


<br/>

Refer to the screen shot below, and add your Masternode information on the 3rd line. Take care that you have added the proper spaces sections 1, 2, 3, and 4. Also, verify that you have appended `:7112` to the end of your IP Address, and that there is a space at the end between your collateral tx id and index (the index will be either a `0` or a `1`).

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/mnconf.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

<br/>

Once you've double checked the entries, save the file, and close out of your editor. 

Go back to the $Pac Desktop Wallet, and close out of the program. Start your $Pac Desktop Wallet program so that it can read the configuration information for your newly configured remote MN. 


In the next step, we will start and broadcast our Masternode onto the network.


# Remote Start Your Masternode

Once you restart your desktop wallet, go to the "Masternodes" tab. From there you should see your newly configured Masternode displayed in the table as shown below:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/mn-tab2.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>


(1). This is the alias you configured previously ("MyMN1" in the screen shot).
<br/>

(2). This is your remote MN's vps IP Address with `:7112` appended at the end.
<br/>

(3). This is your **Unique** MN Receive address where your Masternode Rewards will be paid to as configured in [Configure Desktop: Create Unique MN Wallet Address]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/configure-desktop/#create-unique-mn-wallet-address).
<br/>


<br/>
Follow these steps which will send a "start" your Masternode on the $Pac network as well as broadcast out to the network your MN's IP Address and collateral tx id (needed for validation).


- 1\. Select your Masternode in the Masternode's table.
- 2\. Click the "Start Alias" button:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/mn-tab3.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

- 3\. Select "Yes" and enter your wallet passphrase when prompted and hit ok.


<br/>

Now that we've started our Masternode, let's check to make sure that it has properly started on the remote vps.



<div class="callout callout--warning">
    <p>
    <strong>DO NOT EVER LOOK AT THE STATUS FIELD ON YOUR DESKTOP WALLET!!!! IT IS EVIL!!!</strong>
    Well, not evil, just wrong, most of the time. There is a known bug that will be addressed in future updates (inherited from the Dash wallet), and the status displayed on your desktop wallet is wrong so often that you shouldn't even look at it. I personally don't even see it anymore, its that much out of my consciousness.
    </p>
</div>



# Verify Your Masternode Status

Go back to your ssh client and copy/paste the following into your terminal:

<div class="example" >Check MN Status
</div>
```bash
./paccoin-cli masternode status
```

If you used the copy icon, you can simply paste using - Windows: Ctrl+V or Mac: Command+V into your ssh client.
Otherwise press enter to continue. You should see something similar to the screen shot below. 

Make sure that the status says "Masternode successfully started":

<br/>
<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/mn-status.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

# Next Step: Monitor Your Masternode

Your Masternode is now up and running! Our next step is to [Monitor Your Masternode]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/monitor-mn) and collect rewards.



