!SLIDE subsection
# puppet at mediatemple #

!SLIDE bullets incremental

# Quick history #

* 3 years ago: first commit
* year and a half ago: training
* last year: major systems

!SLIDE center

## &lt;graph of puppet related commits&gt; ##

!SLIDE bullets incremental

# Puppetmaster setup #

* Apache/Passenger
* HA pair of servers using LVS
* GlusterFS to sync puppet data
* Puppet data is managed by packages

!SLIDE center

# Puppetmaster setup #

![puppet.com](puppet_master.png)

!SLIDE bullets incremental

# Puppet development #

* No puppetmaster
* Puppet data installed via packages
* Puppet run done with *prun*
