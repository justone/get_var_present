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

!SLIDE small
# Configuring build warnings #

    @@@ puppet
    class build_server {
        $email = 'nate@mediatemple.net'

        file { '/etc/ci/users/nate.xml':
            content => template('build_server/user.xml.erb')
        }
    }

!SLIDE small
# Configuring build warnings #

    @@@ puppet
    class build_server {
        $email = get_var('users', 'nate_email')

        file { '/etc/ci/users/nate.xml':
            content => template('build_server/user.xml.erb')
        }
    }

!SLIDE small
# Configuring build warnings (2) #

## development ##

    users/var_dev/main.yml
    ---
    nate_email: ""

## production ##

    users/var/main.yml
    ---
    nate_email: nate@mediatemple.net

!SLIDE small
# Configuring nagios user #

    @@@ puppet
    class nagios_server {
        $email = 'nate@mediatemple.net'

        file { '/etc/nagios/users/nate.xml':
            content => template('nagios_server/user.xml.erb')
        }
    }

!SLIDE small
# Configuring nagios user #

    @@@ puppet
    class nagios_server {
        $email = get_var('users', 'nate_email')

        file { '/etc/nagios/users/nate.xml':
            content => template('nagios_server/user.xml.erb')
        }
    }

!SLIDE small
# Configuring webserver proceses #

    @@@ puppet
    class web_server {
        $spare_servers = 40

        file { '/etc/web/server.conf':
            content => template('web_server/server.erb')
        }
    }

!SLIDE small
# Configuring webserver proceses #

    @@@ puppet
    class web_server {
        $spare_servers =
            get_var('web_server', 'spare_servers')

        file { '/etc/web/server.conf':
            content => template('web_server/server.erb')
        }
    }

!SLIDE small
# Configuring webserver proceses (2) #

## development ##

    web_server/var_dev/main.yml
    ---
    spare_servers: 2

## production ##

    web_server/var/main.yml
    ---
    spare_servers: 40

