# F.A.Q.

## Is AutoKiller a task killer?

The main functionality is a minfree manager (see theory section) which tweaks system's built in routines. It also features a built in task manager and process killer.

## How does it work?

Please check [theory/technical details](details.html "theory") part of this site, [this](http://androidforums.com/eris-all-things-root/158846-autokiller-vs-setcpu.html#post1452069) is also a good reading.

## Why is it good to me?

Tasks are handled by the os, apps you no longer use will be cleared up in the background, no user interaction needed.

## How shall I use it?

Check out the great article on [Geek For Me](http://geekfor.me/faq/autokiller/).

## I heard android handles free memory well, why should I keep free memory?

Actually android does a [great job](https://www.youtube.com/watch?v=ITfRuRkf2TM) with memory handling, and free ram is filled with cache immediately. So you have nothing such as "free" ram.

## Application says root access needed. What is it and how can i get it?

Root access means you have superuser (su) permissions on your phone (only su can modify some parts of the system). To achieve it you have to make some modifications on your phones software which may hurt your guarantee, on the other side it will make it available to install custom ROMs, do full system backups, tether your internet, install applications to sd, run AutoKiller (and many other su related apps), and much more (check [this](http://www.androidcentral.com/rooting-it-me-some-qa), [this](https://lifehacker.com/5342237/five-great-reasons-to-root-your-android-phone) and [this](http://androidsocialmedia.com/developments/android-g1-root-access-why-how)). The internet is full with descriptions how to root your phone, you shall just google for it, or start [here](http://theunlockr.com). You can also check [this](http://matrixrewriter.com/wiki/tiki-index.php?page=Root+%26+rooting+your+phones) wiki for more info.

## I set a minfree preset but my free memory doesn't alway get above the settings/I still have empty apps, etc...

Unused ram is wasting of resources, so android (and the linux kernel it is built on) handles stuff wisely. AutoKiller is not killing applications meaninglessly to reach the tresholds but leaves the cleanup to the system which does it properly. My best advice is to stop checking free ram, just enjoy the smooth and lag free behavior even when your device was not rebooted for weeks.

## I heard that killing applications is unnecessary on an android device, so why should I use AutoKiller?

Unfortunately there are many applications which cannot sleep properly, or don't release resources. (the most annoying I met with was a task killer!!!) if you have the time to find out which are these one bye one, you can kill them any time you finish using them. But if you don't want to mess with this, setting lowmemory killer is the best approach as a fix.
"free" memory is not useless: memory is always filled up with cache of your most used applications. So you get resource-consuming applications killed, and got cache with preloaded data your phone will probably use.

## Which is the best setting?

It depends on how you use your phone, you shall discover the best for your device, start with presets and fine-tune manually.

## I clicked on Keep alive/Lower oom, but this setting is not kept. Is the app working wrong?

Actually what this function does is that it sets the process' oom value to the lowest possible value (-17) so it will be the last in the list of killable processes. This doesn't mean it won't be killed, but the possibility is lowered. An other fact is that oom is set by the system, usually when an activity comes to front, and sometimes also in other cases, so there is no possibility to keep this setting over sessions. Conventional keep alive function therefore will never be implemented.

## I set up AutoKiller and it killed my Clock/Twitter/etc...

If you set really high values, it can happen that empty apps like stock android clock in background get killed. My advise in this situation is to lower the limits/choose a lower preset (-you can create direct shortcuts on your desktop to set a preset). You can also make sure that clock is running during the night if that is the last app opened before the phone is sent into sleep mode.

## I have donated and would like to set up alternate preset option properly...

My suggestion is to set AutoKiller to one preset lower than you would withouth this feature, so it can play nice while you use it, and set the alternate preset option to something higher, to make it clean apps in bg in case it is needed while your phone's screen is turned off. In case of my N1 I set AutoKiller to 'Aggressive' and alternate preset to 'Ultimate'. For devices with less available ram you shall choose lower values accordingly.

## What is Chuck Norris mode? When shall I use it?

Chuck Norris mode uses system's built in kill command to terminate the selected application. This is an aggressive way to close running applications, and lets you kill \*\*any\*\* running app. Including dialer and system which can lead to a quick system restart. Use this only if you know what you are doing.

