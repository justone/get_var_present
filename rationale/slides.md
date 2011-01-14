!SLIDE  subsection
# why was this created? #

!SLIDE small
# Creating a database user #

    @@@ puppet
    class db_server {
        $db_username = 'app'
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
        $db_username = 'app'
        $db_password = 'supersecret'

        file { '/etc/app/access.yml':
            content => template('db_client/access.erb')
        }
    }

!SLIDE bullets incremental
# Problems #

* Username/password is duplicated
* Doesn't use a different value for development
* Production password is in source control

!SLIDE small
# Configuring build warnings #

    @@@ puppet
    class build_server {
        $error_email = 'builderrors@company.com'

        file { '/etc/ci/config.xml':
            content => template('build_server/config.erb')
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
        $process_count = 40

        file { '/etc/web/server.conf':
            content => template('web_server/server.erb')
        }
    }

!SLIDE bullets incremental
# Problems #

* Difficult to use a different value for development

!SLIDE bullets incremental

# Solution needed #

* Support different values for development/production
* Production secret values out of source control
* As much data as possible with puppet module
