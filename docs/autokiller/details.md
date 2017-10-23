# Theory / Technical details

## Information about the settings we tweak

Most of the following information are copied from various forums from XDA or MoDaCo, credit goes to original writers.


**Here the long story:** I just was curious if already someone tried to play around with Android's internal low-memory task killer.
We all know that Android uses a different way of handling processes. Instead of killing every process after its Activity ended, processes are kept until the system needs more memory. These processes usually should not harm the overall performance and should give speed improvements if you start an Activity again. That's the idea.
But when does Android kill a process? And which process? As far as I understood android keeps a LRU (last recently used) list and starts killing the oldest unneeded process. This way it is much smarter than any of the taskkillers we see in the Market.
Just for curiosity I started to investigate how this mechanism works. Please correct me if you think that I got something wrong:
**What I found out:** ActivityManagerService.java tracks the "importance" of processes (is foreground, is running a service, ..) and reflects this importance by setting the "oom\_adj" value of the process.
*(For info: "oom\_adj" is a value of every process under Linux which gives the kernel a hint, which process it can kill in an oom \[out of memory\] situation. You can see this value on every Linux 2.6 system in the proc directory: /proc/\[PID\]/oom\_adj ). The higher this value is set, the more likely this process gets selected by the kernel's oom killer.)*
It seems that on Android the current forefround application gets an oom\_adj value of 0 and as soon it's not visible anymore it gets some higher value. I assume the concrete value is dependent by the processes' place in the LRU list.
The out-of-memory killer in the standard Linux kernel only runs in one situation: when the available memory is critical low. However in the Android Linux kernel there is implemented a more fine-grained handling of low memory situations.
I found the kernel source file "**lowmemorykiller.c**" (located in the kernel source tree under "drivers/misc/"; or look here for GIT source tree: tinyurl.com/lowmemkiller).
This module seems to be more configurable than the kernel's standard out-of-memory killer as you can define more than one memory limit, when it should get active and you can tell it which oom\_adj values it may kill.
In other words: You can say "*if free memory goes below XXXX then kill some process with oom\_adj greater then YYY; if free memory goes even more below than ZZZ then start to kill some processes with oom\_adj greater than XYXY. and so on..*"
So it's possible to define multiple memory criterias and matching processes which can be killed in these situations. Android seems to group running processes into 6 different categories (comments taken out of "ActivityManagerServer.java"):
    FOREGROUND_APP:
        // This is the process running the current foreground app.  We'd really
        // rather not kill it! Value set in system/rootdir/init.rc on startup.

    VISIBLE_APP:
        // This is a process only hosting activities that are visible to the
        // user, so we'd prefer they don't disappear. Value set in
        // system/rootdir/init.rc on startup.

    SECONDARY_SERVER:
        // This is a process holding a secondary server -- killing it will not
        // have much of an impact as far as the user is concerned. Value set in
        // system/rootdir/init.rc on startup.

    HIDDEN_APP:
        // This is a process only hosting activities that are not visible,
        // so it can be killed without any disruption. Value set in
        // system/rootdir/init.rc on startup.

    CONTENT_PROVIDER:
        // This is a process with a content provider that does not have any clients
        // attached to it.  If it did have any clients, its adjustment would be the
        // one for the highest-priority of those processes.

    EMPTY_APP:
        // This is a process without anything currently running in it.  Definitely
        // the first to go! Value set in system/rootdir/init.rc on startup.
        // This value is initalized in the constructor, careful when refering to
        // this static variable externally.

These 6 categories are reflected by 6 memory limits which are configured for the lowmemorykiller in the kernel.
**Fortunately, it is possible to configure the lowmemorykiller at runtime! :)** (But only if you are root). The configuration is set in the file: "/sys/module/lowmemorykiller/parameters/minfree"
So if you want to see the current settings, you can do:
`# cat /sys/module/lowmemorykiller/parameters/minfree` This should produce output like this (or similiar): `1536,2048,4096,5120,5632,6144`
These values are the 6 memory limits on which Anedroid starts to kill processes of one of the 6 categories above. Be careful, the **units of these values are pages**!! 1 page = 4 kilobyte.
So the example above says that Anddroid starts killing EMPTY\_APP processes if available memory goes below 24MB (=6144\*4/1024). And it starts to kill unused CONTENT\_PROVIDERs if available memory goes below 22MB (=5632\*4/1024).
So if you want to try if your Hero goes faster when fewer processes are running you can try to adjust these settings. For example if you practically do not want any empty processes you can set the corresponding value very high. For example, you can set the values like this:
`# echo "1536,2048,4096,5120,15360,23040" > /sys/module/lowmemorykiller/parameters/minfree`
This example will tell Android to kill unused Content providers if less then 60MB is available and kill empty processes if available memory goes below 90MB.
All other processes will stay untouched! Do you see the advantage compared to process killers?
One word about durabilty: If you change the settings like this, they are **NOT PERMANENT**. They will be gone after the next restart of your phone. So you can try to play around a little bit.
[source: XDA](https://bit.ly/xdamemory)


