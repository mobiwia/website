# Advanced system tweaks

AutoKiller Memory Optimizer sports experimental kernel tweaks for expert users, applying these should improve overal system responsiveness and boost performance. These settings may not fit every devices well so please handle them with care, and experiment which settings works best for you.
Here you find a few details about each settings:

!!! info "SD card"
    SD readahead parameter is set to a more comfortable value, this speeds up SD card reading by up to 2-3x.

!!! info  "IO scheduler"
    This setting optimizes CFQ IO scheduler and sets kernel values specific for flash storage. Defaults are optimized for spinning harddisks. Lowered the idle wait, re-enable the low latency mode of cfq, removed the penalty for back-seeks and explicitly tell the kernel the storage is not a spinning disk, etc.

!!! info "Partitions"
    Remount all partitions with noatime to reduce write costs.

!!! info "Memory management"
    Set tendency of kernel to swap to minimum, since we don't use swap anyway. Lower the amount of unwritten write cache to reduce lags when a huge write is required. Increase tendency of kernel to keep block-cache to help with slower RFS filesystem. Increase minimum free memory, in theory this should make the kernel less likely to suddenly run out of memory.

!!! info "Scheduler"
    Make the task scheduler more 'fair' when multiple tasks are running. This has a huge effect on UI and App responsiveness. These values (less aggressive settings) are 20% of the Linux defaults, and about half of the Android defaults.

!!! info "Battery"
    Increase the write flush timeouts to save some battery life.

!!! info "Sleeper"
    Disable normalized sleeper. (The normalized sleeper attempted to balance sleeping tasks and wait times to guarantee fairness when used in conjunction with FAIR\_SLEEPERS/GENTLE\_FAIR\_SLEEPERS.)

!!! info "UI"
    Increases "maximum-events-per-sec" to 60 for smoother Homescreen scrolling and transitions.

!!! info "Network"
    Reduces wifi scanning to every 30 secs and optimizes TCP parameters for higher throughput and lower latency when accessing network.

!!! info "Wifi"
    Reduces wifi scanning to every 3 mins (default can be as low as 5 sec) saving battery, this only affects the case in which there are remembered access points, but none are in range.

Credits go to [kernel tweaks](https://forum.xda-developers.com/showthread.php?t=813309) , [SS4N1](https://forum.xda-developers.com/showpost.php?p=11496754) , [SD readahead](https://forum.xda-developers.com/showthread.php?t=1010807)


