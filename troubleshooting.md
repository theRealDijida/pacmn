---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Trouble Shooting
description: 


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: "/"
        url: '/'
    next:
        content:
        url: 

# disqus
comments: true
---

<br/>

See below for a list of helpful commands as well as a section on troubleshooting your $Pac Masternode if you run into problems. This section will continually evolve over time, so if you have suggestions, let me know.

# Helpful Commands

## Checking Your Masternode Status

- Checking the status of your Masternode on your VPS, copy/paste (or type) the following:


```bash
./paccoin-cli masternode status
```
<br/>

- Using a web monitor, see the section [Monitoring Your Masternode]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/monitor-mn/#pac-masternode-monitoring-websites)

- Using the Desktop Wallet: **_DON'T DO IT!!!_**

## Checking Synch Status

- On your vps, copy/paste (or type) the following:


```bash
./paccoin-cli mnsync status
```

The first line of the output should say `AssetId` : `999` when it is fully synched.

<br/>

## Checking to see if the $Pac Masternode process is running

The $Pac MN daemon process is named `paccoind`. To see if it is running use any of the following methods:

- Copy/paste (or type) the following:

```bash
ps aux | grep pacc
```

You should see one entry for the `paccoind` process

- Copy/paste (or type) the following:

```bash
./paccoin-cli masternode status
```

or any of the `paccoin-cli` commands. This will attempt to connect locally to the running `paccoind` process and will return an error if it is not running.

- If you had installed the `systemd` service as explained in the section [Install $Pac MN Service]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/install-server/#install-pac-mn-service) copy/paste (or type) the following:


```bash
systemctl status pacd.service
```

You will need to Ctrl+C to break out and return to the command prompt.

## Checking to see if Sentinel is installed

As mentioned previously in the guide, the `sentinel` process is installed as part of the master $Pac install script. A cron entry is created so that every minute the sentinel process runs to broadcast your MN's status to the $Pac network. To check to see if it has been properly installed, copy/paste (or type) the following on your vps:


```bash
crontab -l
```
you should see the following output:
```
* * * * * cd ~/sentinel && ./venv/bin/python bin/sentinel.py 2>&1 >> sentinel-cron.log
```
If you don't see an entry like above, then sentinel wasn't properly installed. You may need to reinstall your MN.

# Trouble shooting

Some common trouble shooting scenarios are found below:

## New Masternode Status is WATCHDOG

- Make sure that your MN collateral has at least 15 confirmations. 
- Did you [Remote Start]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/start-mn/#remote-start-your-masternode) your Masternode?
- Wait 15-20 minutes after remote starting your MN, and check your status again using the web based monitoring sites. It usually takes this long for the network to synchronize and validate your masternode.
- If after 15-20 minutes, your MN status (using the web based monitor and **NOT YOUR DESKTOP WALLET**) `sentinel` may not be properly installed (see above). If not, you may need to reinstall your MN.

## Masternode Status is NEW START REQUIRED

- Did you check the status using the web based monitoring sites? If you are seeing this in your desktop wallet's Masternode tab, **IGNORE IT**, and check the web based monitors in the section [Monitoring Your Masternode]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/monitor-mn/#pac-masternode-monitoring-websites).
- If the web based monitoring sites indicate that your MN is in NEW START REQUIRED, your MN's `paccoind` process may not be running. Check the status using the commands in the previous section.
- If your `paccoind` process isn't running, you can:
    - [install the systemd service]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/install-server/#install-pac-mn-service), which is highly recommended, as it will bring your process back up (and on reboot) if it ever goes down.
    - If you choose not to install the systemd service, then you can bring your process up by copy/paste (or typing):
```bash
sudo ~/paccoind
```
    - Check that `paccoind` is running as explained in the earlier section.

- Make sure you have sufficient memory (at least 1GB) **AND** swap space to avoid out of memory errors. If you haven't already, you can copy/paste the command below to create swap space for your server:
```bash
sudo fallocate -l 4G /swapfile && chmod 600 /swapfile && mkswap /swapfile && swapon /swapfile && echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab && free -h
```

- Once you get your `paccoind` process back up and running, you'll need to issue a [Remote Start]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/start-mn/#remote-start-your-masternode) of your MN from your desktop wallet. Unfortunately, this will also start your Masternode **_As If_** it were a new Masternode, meaning, you will first have to achieve `Active Time` before becoming payable.
- Check the web based monitors after 15 minutes to make sure that your MN is in `ENABLED` state.


## Masternode Status is EXPIRED

Follow the same steps to trouble shoot above for when your MN is showing `NEW START REQUIRED`

## My MN Isn't Getting Paid

- Using the web based monitors (or mobile apps) is your MN's status `ENABLED` (required).
- Is your MN's position using the web based monitor in the payable pool? 
- The payment logic for the payable pool is random with increasing probability of selection, you can find more information [here](https://docs.dash.org/en/latest/masternodes/understanding.html#payment-logic){:target="_blank"}.
- See stats from [Masternodes Online](https://masternodes.online/currencies/PAC/){:target="_blank"}. These are updated **_and_** an average. For example, if the average payout cycle is 9 days, your MN's current reward cycle may go longer, or shorter. Be sure that it is in the correct status of `ENABLED` and your MN will eventually get paid. Over time, your own average cycle time should converge to the network average.

## I Need to ReHost or Rebuild My MN

Follow these steps if you need to migrate your $Pac MN to another VPS instance or if you are rebuilding onto another server with a _different_ ip address:

1. Shut down your old VPS instance. Eventually, your old IP Address will show `EXPIRED` on the monitoring sites.
2. Install the $Pac MN server just like you would a _New MN_ with the following differences:
    - Keep the **_existing_** Private Gen Key when you setup on your new vps.
    - Update your Desktop Wallet's `masternode.conf` file and change **_only_** the IP Address to the IP Address of your new vps instance. Restart the desktop wallet to pick up the new configuration. 
    - Install everything the same on the vps server as if it were new
    - Remote Start your new vps from the desktop wallet
    - Check the status on the new vps instance: Copy/paste (or type) the following:
```bash
./paccoin-cli masternode status
```
3. On your vps as a result of the above command, you may see something like 'invalid IP Address' or 'rebroadcast new IP Address'. Wait 10-15 minutes and check status again. It will take a while for the new IP Address to propagate through the network. If after 20 minutes, you still don't get a valid status, choose `Start Alias` again from your desktop wallet.



# Suggestions?

Hit me up on discord or add a comment below if you have any suggestions to be added to this guide. $Pac is Community!

