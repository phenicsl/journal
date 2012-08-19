Notes
=====

Load Average
------------

CPU load average is a metric used to determine CPU usage in Linux. CPU load is a
measure of the number of processes that are running as well processes that are
waiting for CPU access. Tracking CPU load averages over a period of time can
help system administrators diagnose the cause of server slowdowns.

To keep track of your system's CPU load average you will need to install the sar
program. This program is usually found in `sysstate` package. It actually will
include following command:

- `sadc` is used to collect system stat information into a specific file,
  ``/var/log/sysstat/saXX`` on debian system.
- `sadr` is used to collect and also display system stat information.
- `sa1` is a shell procedure variant to `sadc` command
- `sa2` is a shell procedure variant to `sadr` command

Once `sysstate` is installed, `sd1` will be configured to run at periodic
intervals via a cronjob, it actually will use `sadc` to do its job. 

On the other hand, `sadr` is a powerful tool, it could be used to read and
display information collected by `sdac`, or you may use it to collect and
display stat information for a period. 

`sadc` is a guard on its duly every day, and `sdar` is more like a ranger.


Memory Usage
------------

`Buffer cache` is an area of free physical memory utilized by the kernel to
store data that has been recently read from a disk and/or utilized by a program,
or that is ready to be written to the disk.


Process
-------

Process may have following stats:
- TASK_RUNNINGtask (process) currently running
- TASK_INTERRUPTABLEprocess is sleeping but can be woken up (interrupted)
- TASK_UNINTERRUPTABLE  process is sleeping but can not be woken up (interrupted)
- TASK_ZOMBIEprocess terminated but its status was not collected (it was not waited for)
- TASK_STOPPEDprocess stopped by a debugger or job control
- TASK_SWAPPING(removed in 2.3.x kernel)




Cookbooks
=========

Delete Entry from cscope.files
------------------------------

When generated cscope files by *find* command, there are some symbol link that
will be warned with "can not find file" error. Following process will help to
get ride of those annoying errors::

    for entry in /path/to/file1 /path/to/file2
    do
        entry=$(echo entry | sed -e 's#/#\\/#')    #escape '/'
	sed -i -e "/$entry/d" cscope.files
    done

Firstly, you have to escape '/' character since *sed* requires to use '/' as
delimiter in the address part. 

Secondly, a in-place edit option is specified here to replace 'cscope.files' in
place. 

After some study, I also found that you may use *"\%$entry%d"* here to specify
the address without escaping the path delimiter.

