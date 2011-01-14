!SLIDE  subsection
# get\_var #

!SLIDE bullets incremental
# get\_var call #

* $variable = "value"
* $variable = get\_var("module", "key")

!SLIDE
# File structure #

    .
    ├── README
    ├── depends
    ├── files
    ├── manifests
    │   └── init.pp
    ├── templates
    ├── var             <- production values
    │   └── main.yml
    └── var_dev         <- development values
        └── main.yml

!SLIDE
# File contents #

## Plain old YAML ##

    ---
    key: value

!SLIDE 
# get\_var #

    @@@ puppet
    $variable = get_var("module", "key")
    
!SLIDE 
# get\_var #

    @@@ puppet
    $variable = get_var("module", "key")
    
    module/var/main.yml in production

!SLIDE 
# get\_var #

    @@@ puppet
    $variable = get_var("module", "key")
    
    module/var/main.yml in production
    module/var_dev/main.yml in development

!SLIDE 
# get\_var #

    @@@ puppet
    $variable = get_var("module", "key")
    
    module/var/main.yml in production
    module/var_dev/main.yml in development

    ---
    key: value

!SLIDE 
# get\_var #

    @@@ puppet
    $variable = get_var("module", "key")
    
    module/var/main.yml in production
    module/var_dev/main.yml in development

    ---
    key: value

    $variable = "value"

!SLIDE bullets incremental
# get\_var key variations #

## "key" ##

    module/var/main.yml
    ---
    key: value

## "file:key" ##

    module/var/file.yml
    ---
    key: value

!SLIDE bullets incremental
# get\_var key variations #

## "file:key.subkey" ##

    module/var/file.yml
    ---
    key:
      subkey: value

!SLIDE small
# Configuring webserver proceses #

    @@@ puppet
    class web_server {
        $process_count =
            get_var('web_server', 'process_count')

        file { '/etc/web/server.conf':
            content => template('web_server/server.erb')
        }
    }

!SLIDE small
# Configuring webserver proceses (2) #

## development ##

    web_server/var_dev/main.yml
    ---
    process_count: 2

## production ##

    web_server/var/main.yml
    ---
    process_count: 40

