# Setup Notes

1. Install on Ubuntu

```
sudo apt-get install postgresql
```

2. Now if you try running psql, you will see an error, where username
is your username

```
PostgreSQL error: Fatal: role “username” does not exist
```

Basically, we need to setup your username in postgres, which can be done using
this command where username is your username

```
sudo -u postgres createuser username
```

and now create a database with the same name as your username

```
sudo -u postgres createdb -O username username
```

Now when you run psql/pglci, you get the prompt.

For app development, you create your app database using your username.
For example, if you want a database called tododb, do the following

```
sudo -u postgres createdb -O username tododb
```

Now you can connect to the database 

```
psql -d tododb
```

You can now set an environment variable for DATABASE_URL

```
export DATABASE_URL=postgres://tododb
```

