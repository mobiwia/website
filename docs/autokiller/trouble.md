# Troubleshooting

## What to check if something doesn't work

Please check this list before reporting any problems, most cases can be solved easily

-   Do you have the latest version of the app? -&gt; check market
-   Is your phone rooted? (do you have other root dependent apps working?)
-   Have you given root permissions to AutoKiller? (you can check this if you start 'Superuser' application)
-   Superuser app sometimes cannot grant su rights on boot, check [SuperSU](https://play.google.com/store/apps/details?id=eu.chainfire.supersu)
-   Is AutoKiller on phone memory? It won't restore settings if it is on SD.
-   Please try an uninstall - reboot - reinstall cycle.
-   Have you read the [faq?](faq.md "faq")

## PRO application cannot validate?

-   Try uninstalling both free and pro apps, reboot your device and reinstall from the [web-based Play Store](https://play.google.com/store/search?q=mobiwia&c=apps) (hacky workaround)
-   Check if market can reach the internet
-   Check your firewall settings
-   Are free and pro versions both on phone memory? Don't move to SD.
-   Remove/disable any tampering apps (Lucky patcher, some Xposed modules, ...)
-   Are "Background Sync" & "Auto Sync" (Settings/Accounts & Sync/Background Data) enabled?

If none of the above apply please collect a logcat about the error and send it to me.
[about](https://developer.android.com/intl/fr/guide/developing/tools/adb.html#logcat) [logcat](http://wiki.cyanogenmod.com/index.php?title=Logcat)
