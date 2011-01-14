!SLIDE  subsection
# common facilities #

!SLIDE
# Production or Development #

## /etc/puppet/master.yml ##

    ---
    environment: production

!SLIDE bullets incremental
# key variations #

## "key" ##

    module/var/main.yml
    ---
    key: value

## "file:key" ##

    module/var/file.yml
    ---
    key: value

!SLIDE bullets incremental
# key variations #

## "file:key.subkey" ##

    module/var/file.yml
    ---
    key:
      subkey: value

!SLIDE bullets
# Default values #

* $variable = get\_var("module", "key", "default")
* $variable = get\_secret("module", "key", "default")
