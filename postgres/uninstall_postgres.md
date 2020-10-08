# Uninstall Postgres


```
$ sudo apt-get --purge remove postgresql
```

Now check what other postgres packages are installed

```
dpkg -l | grep postgres
```

This will list any other packages still installed, which can be
removed using this command where {package name} is the package
still installed

```
sudo apt-get --purge remove {package name}
```

Now delete all remaining remnants

```
$ sudo rm -rf /var/lib/postgresql/
$ sudo rm -rf /var/log/postgresql/
$ sudo rm -rf /etc/postgresql/
$ sudo deluser postgres
$ sudo delgroup postgres
```


