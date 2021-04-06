# Apt Update Failing

Today when I was running `sudo apt update`, I saw some failures

```
$ sudo apt update
...
Err:13 http://packages.cloud.google.com/apt cloud-sdk-bionic InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
...
W: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. GPG error: http://packages.cloud.google.com/apt cloud-sdk-bionic InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Failed to fetch http://packages.cloud.google.com/apt/dists/cloud-sdk-bionic/InRelease  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY FEEA9169307EA071 NO_PUBKEY 8B57C5C2836F4BEB
W: Some index files failed to download. They have been ignored, or old ones used instead.
```

This is because the cloud-sdk gpg keys you added have expired. You can check by running `sudo apt-key list`

```
$ sudo apt-key list
/etc/apt/trusted.gpg
--------------------
pub   rsa2048 2018-04-01 [SCEA] [expired: 2021-03-31]
      54A6 47F9 048D 5688 D7DA  2ABE 6A03 0B21 BA07 F4FB
uid           [ expired] Google Cloud Packages Automatic Signing Key <gc-team@google.com>

pub   rsa2048 2015-04-03 [SCEA] [expired: 2018-04-02]
      D0BC 747F D8CA F711 7500  D6FA 3746 C208 A731 7B0F
uid           [ expired] Google Cloud Packages Automatic Signing Key <gc-team@google.com>
...
```

To delete these expired keys, just take the last 8 characters of the key to reference which key to delete - 

```
$ sudo apt-key del BA07F4FB
OK
$ sudo apt-key del A7317B0F
OK
```

Now re-add your gpg keys for the provider. Depending on your version of apt you may have to adjust the command

```
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
```

or

```
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

That should fix `sudo apt update`
