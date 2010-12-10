This is a collection of plug-ins aimed at monitoring instances of Escenic Content Engine.

They are licensed under a BSD license.

  escenic_heap_   -- contrib family autoconf and suggest capable.
  escenic_utilization_ -- manual contrib family autoconf and suggest capable.  Requires port number.

Have fun with them!


Here's a heap graph.  It shows the different parts of the JVM memory so you can see what needs tuning.

!(heap graph)[https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_heap-day.png]

Here's a couple of GC graphs that show you how many garbage collections that are happening per minute, and how much CPU is used doing just that:

Garbage collections per minute

!(Line graph showing about 100-150 garbage collections per minute over a 30-hour period)[https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_gc-day.png]

Percent of CPU or rather time used in garbage collection

!(line graph with percent on Y-axis and time on X-axis, showing 10-50 milli-percent over a 30-hour period)[https://github.com/mogsie/escenic-munin/raw/master/site/escenic_jstat_baz_gcoverhead-day.png]

