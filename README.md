This is a collection of plug-ins aimed at monitoring instances of Escenic Content Engine.

They are licensed under a BSD license.

 * escenic\_jstat\_   -- contrib family autoconf and suggest capable.
 * escenic\_utilization\_ -- manual contrib family autoconf and suggest capable.  Requires port number.

Have fun with them!


##escenic\_jstat\_

### Installation

     curl https://github.com/mogsie/escenic-munin/raw/master/escenic_jstat_ |
          sudo tee /usr/share/munin/plugins/escenic_jstat_
     chmod 755 /usr/share/munin/plugins/escenic_jstat_
     sudo munin-node-configure --shell | sudo sh

Add it to your /usr/share/munin/plugins/ and run munin-node-configure to get its suggestions running.  It works only if Escenic is running while you do this, since it looks for its pidfiles in /var/run/escenic/.

It suggests four graphs for each instance :\_gc \_gcoverhead \_heap and \_uptime, all prefixed with the name of the instance.

If you need to install the symlinks manually, make a symlink as follows:

     escenic_jstat_default_heap       -> /usr/share/munin/plugins/escenic_jstat_
     escenic_jstat_default_gc         -> /usr/share/munin/plugins/escenic_jstat_
     escenic_jstat_default_gcoverhead -> /usr/share/munin/plugins/escenic_jstat_
     escenic_jstat_default_uptime     -> /usr/share/munin/plugins/escenic_jstat_

If you have more than one pidfile, make another set of links swapping out default with something else.

It uses jstat to run, so you need to tell munin to run this plug-in as the same user as escenic.  So for two instances (default and test), running as different users (escenic and test):

     [escenic_jstat_default_*]
           user escenic
     [escenic_jstat_test_*]
          user test

You might also need to tell it where jstat is:

     [escenic_jstat_*]
          env.jstatbin = /opt/jdk/bin/jstat

If you have pidfiles in non-standard locations or with strange names, you can specify those too:

     [escenic_jstat_default_*]
          env.pidfile = /opt/appserver/run/jvm.pid
     [escenic_jstat_foo_*]
          env.pidfile = /opt/solr/run/solr.pid

##Examples

The example is from a live system, where memory exhaustion became very apparent by looking at how the heap grpahs evolved, and how increasing the heap size fixed the problem.

### Heap graph

Here's a heap graph.  It shows the different parts of the JVM memory so you can see what needs tuning.  On the graph to the left, the heap size increased from 2.0Gb to 2.5Gb, and you can clearly see how this affected the young and old generations.  It is also apparent that before the increase in heap size, the old generation was full.  Indeed, on the graph to the right, on the night between the 20th and 21st, the heap seems to be completely full.

<img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_heap-day.png" width="50%"> <img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_heap-week.png" width="50%">

### Young vs Old GCs

The garbage collection graph shows you how many garbage collections that are happening every minute.  On the graph to the left, the young garbage collector (green) is running at about 10-15 collections per minute, which is about 4-6 seconds between each collection.  However, on the graph to the right, you see that on the night between the 20th and 21st, there was a period of a few hours where the old generation was being collected severely, at the same time that the old heap was "full".  The full collections were running at about 3 or four per minute.

Here's a couple of GC graphs that show you how many garbage collections that are happening per minute, and how much CPU is used doing just that:

Garbage collections per minute

<img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_gc-day.png" width="50%"> <img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_gc-week.png" width="50%">

Percent of CPU or rather time used in garbage collection

<img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_gcoverhead-day.png" width="50%"> <img src="https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_default_gcoverhead-week.png" width="50%>


