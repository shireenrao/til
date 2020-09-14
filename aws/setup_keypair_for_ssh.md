# Setup Keypair for ssh

AWS Cli makes it super easy

Here is how you generate a keypair

```
aws ec2 create-key-pair --key-name keyname
```

This creates a keyname and redirects it to your console. To save the output to a file use this

```
aws ec2 create-key-pair --key-name keyname --query 'KeyMaterial' --output text > mykey.pem
```

These key names are managed under aws. Some commands to manage them

```
$ aws ec2 describe-key-pairs --key-name MyKeyPair # displays the keypair on your console
$ aws ec2 delete-key-pair --key-name MyKeyPair # delete your keypair
```

The pem file should have only read access for your user. Make sure to `chmod 400` the pem file.

To generate the public key for the pem file to be added to the remote .ssh/authorized_keys file,
make sure the .ssh folder permission is set to be only readable and writable by your user. Use following
steps

```
$ chmod 700 .ssh
$ touch .ssh/authorized_keys
$ chmod 600 .ssh/authorized_keys
```

You can retrieve the public key for your keypair with this command

```
$ ssh-keygen -y -f /path_to_key_pair/my-key-pair.pem
```

This will fail if the permissions to the keypair file is not only readable by you. As mentioned above.

Copy the output to the remote servers .ssh/authorized_keys file. 

Now you should be able to ssh to the remote server. 


```
$ ssh -i /path_to_key_pair/my-key-pair.pem remoteuser@remotemachine
```

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html
https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-keypairs.html
https://aws.amazon.com/premiumsupport/knowledge-center/new-user-accounts-linux-instance/
 
