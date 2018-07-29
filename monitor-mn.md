---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Monitor Your Masternode
description: 


# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Start Your Masternode
        url: '/start-mn'
    next:
        content: Next Steps
        url: '/next-steps'

# disqus
comments: true
---

<p>&nbsp;</p>
Congratulations! You've just installed and started your new $Pac Masternode! 

A quick reminder of where we are below:

<b>Steps to create your Master Node</b>

- [x] &nbsp; ~~1. Getting Ready~~
- [x] &nbsp; ~~2. Configure your desktop wallet~~
- [x] &nbsp; ~~. Install Master Node server on your VPS~~
- [x] &nbsp; ~~4. Start your Master Node~~
- [ ] &nbsp; <mark>5. Monitor your Master Node and collect rewards</mark>


<div class="callout callout--info">
    <p>
    Your desktop/cold wallet synchronizes with the $Pac network and its distributed blockchain whenever it is online and connected. Your $Pac Masternode must stay online and connected all of the time in order to provide second tier services to the network. What this means is that you can shut down your desktop/cold wallet for as long as you like, as long as your $Pac MN on your vps is running. This is where monitoring becomes handy and important.
    </p> 
</div>


# $Pac Masternode Monitoring Websites

Next we will use one of the web based monitoring tools for your new $Pac Masternode. The web based monitoring apps are important, and you should get to know them. Not only do they have some important information, but they can also be sent as links to your mobile phone (in addition to the mobile monitoring apps in the next section).
The reason why we want to use a monitor site/app **_AND NOT_** the desktop wallet is because of 2 reasons: 1) Monitoring sites are connected to the network, and now the $Pac network sees your Masternode in terms of status is all that matters in terms of getting rewards (it is after all, a decentralized, quorum based network) and 2) as mentioned previously, the desktop wallet has a known bug that shows the wrong status and it will both freak you out as well as cause constant heartburn looking at it. **_THE DESKTOP WALLET FOR MN STATUS IS EVIL_**. Repeat that again and you will be fine.

In order for your $Pac Masternode to receive its first reward, it has to achieve "Active Time". In addition to being in an **ENABLED** state, Active Time is achieved by being on the network as a new MN for a minimum of X minutes which is calculated as: **X = (Number of MNs) * 2.6 minutes**. So, if your MN is created when there are 5,000 MNs on the network, your new MN will achieve Active Time in 5,000 * 2.6 minutes, or 13,000 minutes or about 9 days and 40 miniutes. Once your Masternode achieves active time, it will be put into *Position #1* in the Payable Pool (more on that later).

Click the following link which will open in a new browser window: [http://pacmaster.nomukaiki.com/](http://pacmaster.nomukaiki.com/){:target="_blank"}. Enter your Masternode's IP Address in the field indicated and click the search button:

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>

This is an excellent web monitor from nomukaiki.

There are a few websites that help you to monitor your $Pac Masternode

- [http://pacmaster.nomukaiki.com/](http://pacmaster.nomukaiki.com/){:target="_blank"}

- [http://monitor.masternodes.work/monitor](http://monitor.masternodes.work/monitor){:target="_blank"}

- [http://stats.foxrtb.com/monitor.html](http://stats.foxrtb.com/monitor.html){:target="_blank"}

You'll want to refer to one of these sites as your MN is running (as well as using the mobile apps in the next section) in order to see the status and position of your Masternode in the Payment Queue (first 2 links). In $Pac Masternode payment logic, each MN that is in **ENABLED** state and **Active** on the network holds a "position" in line for rewards. As each block is mined, and a reward awarded to the selected MN, each Masternode in the queue moves up one position. MN's eligible for payment must be in the front 10% of the queue, known as the "Payable Pool". The nuance here is that this pool is random with increasing probability of being selected the longer an MN is in the pool. So, for example, with 5,000 MNs on the network, the Payable Pool would consist of MN's in position 1-500 (front 10%). Your position once in the payable pool should only be indicative, as MNs may be selected at random as soon as they enter the pool (at position 500 for example), or at any other position (hence the randomness). 

You can find details about the payment logic from the excellent [Dash documentation portal](https://docs.dash.org/fr/latest/masternodes/understanding.html#payment-logic){:target="_blank"}.



# Mobile $Pac Masternode Apps

One of the best ways to monitor your $Pac Masternode on the go is the official $Pac Mobile Masternode Monitoring App. You can find versions for both iOS and Android via the links below:

- [iOS App from iTunes](https://itunes.apple.com/us/app/masternodes-monitor-%24pac-mn/id1387962793?mt=8){:target="_blank"}
<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacmnmobile-ios.jpg" style="display: block;margin-left: auto;margin-right: auto;width: 25%;"/>

- [Androig App from Google Play](https://play.google.com/store/apps/details?id=com.pac.masternodeapp){:target="_blank"}
<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacmnmobile-android.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%;"/>

# Collecting Rewards



# Next Step: Voting and Useful Links

Welcome to the $Pac Masternode community! Next, find out more information on [Voting and Useful Links]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/next-steps).



