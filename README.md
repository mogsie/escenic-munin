This is a collection of plug-ins aimed at monitoring instances of Escenic Content Engine.

They are licensed under a BSD license.

 * escenic_jstat_   -- contrib family autoconf and suggest capable.
 * escenic_utilization_ -- manual contrib family autoconf and suggest capable.  Requires port number.

Have fun with them!


##escenic_jstat_

add it to your /usr/lib/munin/plugins/ and run munin-node-configure to get its suggestions running.  It works best if Escenic is running while you do this, since it looks for its pidfiles in /var/run/escenic/.

It suggests four graphs for each instance :_gc _gcoverhead _heap and _uptime, all prefixed with the name of the instance.

It uses jstat to run, so you need to tell munin to run this plug-in as the same user as escenic.  So for two instances (default and test), running as different users (escenic and test):

     [escenic_jstat_default_*]
           user escenic
     [escenic_jstat_test_*]
          user test

##Examples

Here's a heap graph.  It shows the different parts of the JVM memory so you can see what needs tuning.

![heap graph](https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_heap-day.png)

Here's a couple of GC graphs that show you how many garbage collections that are happening per minute, and how much CPU is used doing just that:

Garbage collections per minute

![Line graph showing about 100-150 garbage collections per minute over a 30-hour period](https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_gc-day.png)

Percent of CPU or rather time used in garbage collection

![line graph with percent on Y-axis and time on X-axis, showing 10-50 milli-percent over a 30-hour period](https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_gcoverhead-day.png)

