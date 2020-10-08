# Trusting Local Development

To allow passwordless logins similar to how macOS postgresapp does it we need to modify
the connection method in the pg_hba.conf file. This file will be under `/etc/postgresql/{version}/main/`

This is what they are before I made the change

```
local   all             postgres                                peer

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 md5
```

and this is after I change the method on these connections to trust

```
local   all             postgres                                trust

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
```
