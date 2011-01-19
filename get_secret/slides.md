!SLIDE  subsection
# get\_secret #

!SLIDE bullets incremental
# get\_secret call #

* $variable = "password"
* $variable = get\_secret("module", "key")

!SLIDE
# File structure #

    .
    ├── README
    ├── depends
    ├── files
    ├── manifests
    │   └── init.pp
    ├── templates
    └── secret_dev         <- development values
        └── main.yml

!SLIDE bullets incremental
# Production secrets #

* Not in *secret/*
* In */etc/puppet/secret/*
* Usually on the puppetmaster

!SLIDE small
# Creating a database user #

    @@@ puppet
    class db_server {
        $db_username = get_var('db_server', 'db_username')
        $db_password = get_secret('db_server', 'db_password')

        db_user { $db_username:
            ensure => present,
            password => $db_password,
        }
    }

!SLIDE small
# Creating a database user (2) #

## development ##

    db_server/secret_dev/main.yml
    ---
    db_password: devdbpass

## production ##

    /etc/puppet/secret/db_server/main.yml
    ---
    db_password: supersecret

!SLIDE small
# Configuring database access #

    @@@ puppet
    class app {
        $db_username = get_var('db_server', 'db_username')
        $db_password = get_secret('db_server', 'db_password')

        file { '/etc/app/access.yml':
            content => template('db_client/access.erb')
        }
    }

!SLIDE bullets incremental
# Deploying production secrets #

* Separate, locked down server
* Rsync secrets to all puppetmasters
