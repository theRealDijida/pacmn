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
Congratulations! You now have your very own brand new $Pac Masternode! 

A quick reminder of where we are below:

<b>Steps to create your Master Node</b>

- [x] &nbsp; ~~1. Getting Ready~~
- [x] &nbsp; ~~2. Configure your desktop wallet~~
- [x] &nbsp; ~~. Install Masternode server on your VPS~~
- [x] &nbsp; ~~4. Start your Masternode~~
- [ ] &nbsp; <mark>5. Monitor your Masternode and Collect Rewards</mark>

<br/>

<div class="callout callout--info">
    <p>
    Your cold wallet (installed on your desktop or laptop) synchronizes with the $Pac network and its distributed blockchain whenever it is online and connected. However, your $Pac Masternode must stay online and connected all the time in order to provide second tier services to the network. What this means is that you can shut down your desktop/cold wallet for as long as you like, as long as your hot wallet on your VPS is running. This is where monitoring becomes handy and important.
    </p> 
</div>

<br/>

When you first create a new $Pac Masternode, it goes through several stages from inception to its first payment. Masternodes have a status on the $Pac network. When they are new, they have the **WATCHDOG_EXPIRED** state for about 15 minutes while the MN's IP Address, Collateral Tx ID are broadcast, validated, and propagated through the network. It will then go to **ENABLED** state. This is the state you want your Masternode to be in **_All the Time_** as it means that it is available to receive reward payments. 

In order for your $Pac Masternode to receive its first reward, it has to achieve `Active Time` status. Active Time is achieved by being on the network in the 'ENABLED' state for a minimum of X minutes which is calculated as: `X = (Number of MNs) * 2.6 minutes`. So, if your MN is created when there are 5,000 MNs on the network, your new MN will achieve Active Time in 5,000 * 2.6 minutes, or 13,000 minutes or about 9 days and 40 miniutes. Once your Masternode achieves Active Time, it will be put into *Position #1* in the Payable Pool. Refer to the diagram below as we walk through the lifecycle of Masternode payments.

<br/>
<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacpayment.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%;"/>


- (1) This is where we are now, your new created $Pac Masternode is brand new on the network, and in about 15 minutes should go to "Enabled" status. As noted previously, **_DO NOT REFER TO YOUR DESKTOP WALLET'S MASTERNODE TAB FOR STATUS!!_**. Instead, we'll use one of the monitoring websites described in the next section.
- (2) Once your new Masternode goes from `WATCHDOG_EXPIRED` to `ENABLED` status, your MN now needs to achieve `Active Time` as described above.
- (3) Now that your new MN has achieved `Active Time`, and is in `ENABLED` status, it will immediately get "pushed" into position 1 in the payable pool, which is the front 10% of enabled MNs active on the network. As an example, if there are 5,000 MNs enabled in the network, the front 10% payable pool would be those MNs in position 1-500. 
- (4) `Quorum` selection for the Masternode to get paid in the next mined block on the block chain uses an algorithm that is random with increasing probability of getting selected based on the amount of time spent in the payable pool. Remember, your position has a relative probability. As new MNs join the network, achieving their own active time, all other MNs will get pushed back 1 in the queue.
- (5) Each block mined on the blockchain distributes 10,350 $Pac to the selected MN for a reward payment, and then every MN in the queue moves up 1 in position.
- (6) Your Masternode gets selected and paid, _Yippeee!!!_. Your MN will now go to the end of the payable queue.

You can find more details about the payment logic from the [Dash documentation portal](https://docs.dash.org/fr/latest/masternodes/understanding.html#payment-logic){:target="_blank"}.

Next let's go to some online monitors where we can check out your new $Pac Masternode's **status** and other statistics.


# $Pac Masternode Monitoring Websites

Next we will use one of the web based monitoring tools for your new $Pac Masternode. The web based monitoring apps are important, and you should get to know them. Not only do they have some important information, but they can also be sent as links to your mobile phone (in addition to the mobile monitoring apps in the next section).
The reason why we want to use a monitor site/app **_AND NOT_** the desktop wallet is because of 2 reasons: 1) Monitoring sites are connected to the network, and how the $Pac network sees your Masternode in terms of status is all that matters in terms of getting rewards (it is after all, a decentralized, quorum based network) and 2) as mentioned previously, the desktop wallet has a known bug that shows the wrong masternode status and it will probably freak you out.


Click the following link (an excellent web monitor from Nomukaiki) which will open in a new browser window: [http://pacmaster.nomukaiki.com/](http://pacmaster.nomukaiki.com/){:target="_blank"}. 

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>

<br/>

Click the search button

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn2.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>

<br/>

Enter your MN's IP Address and select it. You should see something like the screen shot below. (Note, I used random MN's ip address for this example)

<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn3.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%;"/>

<br/>

Here you can see your Masternode's status (If it's in `WATCHDOG_EXPIRED` status, it should go to `ENABLED` in about 15 minutes), as well as the `Time left to be payable`. This refers to the amount of time left to achieve Active Time as explained above. You can also see the number of MNs on the network at the top of the screen, including the number of MNs that are in a payable state. You can bookmark this link and send it to your smart phone which is handy for checking your MN's status when you're on the go.

Another good monitoring site is [http://monitor.masternodes.work/monitor](http://monitor.masternodes.work/monitor){:target="_blank"}:


<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn4.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>

<br/>

as well as [http://stats.foxrtb.com/monitor.html](http://stats.foxrtb.com/monitor.html){:target="_blank"}

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/monitormn5.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%;"/>

<br/>

You'll want to use one of these sites when your MN is running to see the status and position of your Masternode in the Payment Queue. Next, let's check out some mobile apps for monitoring your masternode.

# Mobile $Pac Masternode Apps

One of the best ways to monitor your $Pac Masternode when you're on the go is the official $Pac Mobile Masternode Monitoring App. Once you have your $Pac Masternode in the app, you will be able to see your position and status, as well as getting push notifications when your MN gets paid or enters the payable pool. You can find versions for both iOS and Android via the links below:

- [iOS App from iTunes](https://itunes.apple.com/us/app/masternodes-monitor-%24pac-mn/id1387962793?mt=8){:target="_blank"}
<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacmnmobile-ios.jpg" style="display: block;margin-left: auto;margin-right: auto;width: 25%;"/>

- [Android App from Google Play](https://play.google.com/store/apps/details?id=com.pac.masternodeapp){:target="_blank"}
<br/>

<img src="{% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/images/pacmnmobile-android.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%;"/>

# Next Step: Voting and Useful Links

Welcome to the $Pac Masternode community! Next, find out more information on [Voting and Useful Links]({% if jekyll.environment == 'production' %}{{ site.doks.baseurl }}{% endif %}/next-steps).



