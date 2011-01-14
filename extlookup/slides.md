!SLIDE  subsection
# what about extlookup? #

!SLIDE bullets incremental
# get\_var/get\_secret pros #

* Data is kept with puppet module
* Clear delineation between production and development

!SLIDE bullets incremental
# get\_var/get\_secret cons #

* Lookups don't cascade based on hostname or other facts
* Not included with puppet

!SLIDE bullets incremental
# extlookup pros #

* Included with puppet (as of 2.6.1)
* Cascading lookups

!SLIDE bullets incremental
# extlookup cons #

* Data is managed separately
* Heirarchical data isn't supported
