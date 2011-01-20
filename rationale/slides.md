!SLIDE  subsection
# why was this created? #

!SLIDE small
# Creating a database user #

    @@@ puppet
    class db_server {
        $db_username = 'db123'
        $db_password = 'supersecret'

        db_user { $db_username:
            ensure => present,
            password => $db_password,
        }
    }

!SLIDE small
# Configuring database access #

    @@@ puppet
    class app {
        $db_username = 'db123'
        $db_password = 'supersecret'

        file { '/etc/app/access.yml':
            content => template('db_client/access.erb')
        }
    }

!SLIDE bullets incremental
# Problems #

* Username/password is duplicated
* Production password is in source control
* Doesn't use a different value for development

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
# Configuring nagios user #

    @@@ puppet
    class nagios_server {
        $email = 'nate@mediatemple.net'

        file { '/etc/nagios/users/nate.xml':
            content => template('nagios_server/user.xml.erb')
        }
    }

!SLIDE bullets incremental
# Problems #

* Email address is duplicated
* Difficult to use a different value for development

!SLIDE small
# Configuring webserver proceses #

    @@@ puppet
    class web_server {
        $spare_servers = 40

        file { '/etc/web/server.conf':
            content => template('web_server/server.erb')
        }
    }

!SLIDE bullets incremental
# Problems #

* Difficult to use a different value for development

!SLIDE bullets incremental

# Solution needed #

* Production secret values out of source control
* Support different values for development/production
* As much data as possible with puppet module
