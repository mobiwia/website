# FAQ

## I have no idea how this app is working...

Please read the [User Guide](index.md) to learn how to use it.

<a name="fix"> </a>

## Steps to follow if you have a non-locking GPS

  1.   Side menu / Manage aGPS state.
  2.   Select 'Reset' to clear the internal state of the GPS.
  3.   Select 'Download' to re-download the assistance data. You will need an active internet connection at this step.
  4.   Close the GPS Status application for 10 seconds.
  5.   Go outside and find a spot where large part of the sky is visible.
  6.   Make sure you have the 'Keep the screen on' settings turned on (in Settings / Display & Tools'.
  7.   Let the program run and try to acquire your GPS position for at least 15 minutes.

!!! note
    - If the above steps do not resolve the GPS issue then you most likely have a hardware problem with the phone.
    - Certain phone cases block the GPS signal (remove the phone from it, if you are not sure.)
    - Certain windshields may block the GPS signal inside cars (those that have metallic coating to keep the heat out.)
    - Certain phones (usually CDMA) turn off the GPS chip if you put the phone into flight mode.
    - If you travel a long distance without turning on the GPS (i.e. flight) you can expect much longer fix times at your destination initially.
    - You cannot expect the GPS to work in your basement! (yes I'm serious)

<a name="license"></a>

## I have previously purchased the PRO version, but now I have to reinstall it. How do I re-activate my license?

Purchases on Google Play are bound to your google account. It means that you can activate the license on ALL of your devices as long as they are registered with your google account. You should never ever pay twice for the same thing! Prior to 2016 GPS Status used separate 'key' application for licensing. Starting from the beginning of 2016 in-app payments are used for licensing. First you need to know which type of license you have. The best is to take a look at your purchase history and find GPS Status on [wallet.google.com](https://wallet.google.com). If you have purchased the PRO key application, you can [re-download it again from the Play Store](https://play.google.com/store/apps/details?id=com.eclipsim.gpstoolbox.pro). If you purchased the license as an in-app payment (you will see "PRO Features" in your transaction list), just install and open the main (free) app and tap the 'Get PRO' item in the side navigation menu. Play Store will detect and inform you that you already own this item and GPS Status will activate the license immediately. If you have issues or you have changed your google account for whatever reason, please contact the support address with your original transaction id. 

## I do not like/need the notification when an app accesses the GPS. Can I turn it off?


Yes. GPS Status never runs in the background unless an other app access the GPS. You can turn off the notification feature in 'Settings / Background behavior / Show Notification = Never' and then restarting the app (quitting with the back button and then starting it again).

## The notification sometimes is not sown when Goolge Maps is running.

This is happening on Android 6 and later. Goolge Maps is no longer using the GPS in the phone directly. Instead it's using Google's proprietary "fused location provider". Because of this, GPS is started only occasionally in the background and 3rd party applications are not notified about it. Sadly this cannot be worked around as indeed in these cases GPS is NOT used so there is no point to show the status.

## Why do you need permission XXX?

-   coarse and fine location: we need this to display your location :)
-   full internet access: used by the advertisement and analytics component. 
-   access extra location provider commands: allows the program to re-download AGPS data or reset the GPS.
-   view network state: allows checking if there is an active internet connection. If there is no net connection, advertisement and AGPS download is disabled to save memory and battery.
-   Storage and Media Access:This is need only to be able to Export/Import your stored waypoints to the exteral storage.

## It is eating all my battery according to the battery status screen. It is even running in the background.
Fortunately no. The bug is in the battery measurement routines in Android. The operating system sometimes misses the notification when the application releases the phone sensors (i.e. this issue affects all apps that heavily use the sensor system). Because of the missed "release message" the battery measurement routines continue to count the battery use against the application even if that application was stopped long ago and not even present in the process list. You can simply ignore this. Unfortunately you need to restart the phone to "fix" this malcalculation. Once you've rebooted the phone you will see the correct values again and the "phantom" usage will disappear. The reason why this is increasing over time without even running is that the power usage is calculated for the sensor by (current time - sensor attach time)\*sensorPowerRequirements. As time passes, this value increases.

## The GPS time is 15 seconds ahead of the official UTC time. Why? I thought GPS clocks must be extremely accurate.
The rotation period of the Earth is not constant and in average it is 2ms longer than 86400 sec. This causes some drift over time between the atomic clocks (used by the GPS system) and the UTC time. To avoid confusion, every now and then leap seconds are inserted into the UTC time. (Yes, there are sometimes 61s long minutes!). GPS and UTC was in sync in 1980. Since then 15 leap seconds were inserted into the UTC time. The GPS satellites brodcast this information, but only in every 12minutes. Your receiver may not heard the broadcast, so it does not know how much it should substract from the GPS time. Without this information it just displays the GPS time and does not correct it to get UTC. You should wait at least 15 minutes with the GPS turned on to receive the correction data.

## Some parts of the application are not translated or there are translation errors.
Feel free to join the GPS Status translation project at [crowdin.net](https://crowdin.net/project/gps-status). You can add new translations, or correct existing ones.

## The location/altitude or other data is inaccurate.
GPS Status simply displays the data received directly from the phone hardware. In fact this is the main pupose of the software (that's why it's called status). Inaccurate data is not the fault of the software, but shows that you may not have optimal reception of GPS satellites or there is a magnetic anomaly nearby affecting your compass. Find a different location and try again. If you feel that the data is inaccurate, it may indicate a hardware issue. Please note that the sensors in your phone (including the GPS receiver) are very prone to environmental disturbances.

## My compass is very "jumpy"...
Try to set the sensor filtering in preferences. It can filter out the measurement noise, but at the same time the compass will react slower to changes.

## Is it showing magnetic or true north? How to set the magnetic declination?

Magnetic declination is the difference between the true and magnetic north at your location. The value is calculated automatically by the program using the current geo-magnetic earth model. The algorithm uses your current location and time. To answer the question: The needle in the middle is always showing the magnetic north while the grid itself (small red arrow) points always towards true north. The angle between these two corresponds to the magnetic declination. The last number in the "Magnetic field" instrument is the magnetic declination in degrees.

## My compass points to the wrong direction or I'm asked to calibrate my compass. What should I do?
Your phone contains a digital compass which measures the magnetic field's strength in three direction with three separate sensors. The orientation of your phone is calculated from these values. Unfortunately the sensitivity of the sensors can be a little different. To correctly calculate your orientation your phone must measure first these differences. This is done during the calibration process. To calibrate your phone, simply find a space where no external magnetic field is present (preferable outside of buildings) and rotate your phone 1-2 times on EACH of its three axes. (Swinging your phone in big 8s in all direction will also do, but it's less scientifically correct :) ). If you feel that your compass has become inaccurate you can repeat this procedure. NOTE: You should expect the compass to be very unreliable inside buildings or vehicles often pointing in opposite directions. 

## What does the Magnetic field reading mean?
Aside from your orientation, your phone can measure the absolute strength of the magnetic field which is displayed as the first number in the reading. The second number is calculated from your GPS position and current time using the earth geo-magnetic model. It is the theoretical strengh you should measure in an open space. If the two values are sufficiently different, then you are standing in a magnetic anomaly. This is pretty funny because this allows you to detect big nearby metal objects. Go and try hunting for treasures.

## The compass needle changes its size... What the hell?
The size of the needle indicates the relative magnitude of measured magnetic field to the calculated value. If the measured and calculated value is the same, the needle should be the same size as the inner circle on the grid. If the magnetic field is bigger/smaller than it should be, the needle will be also bigger/smaller. This way you can see at a glance whether you are standing in a magnetic anomaly. If the needle is too small or too big chances are that an external magnetic field is present and the compass points to the wrong direction.


