# Docker on WSL2

I did not want to use Docker Desktop on windows with WSL2. For some reason straightup docker instructions from the [official docs](https://docs.docker.com/engine/install/ubuntu/) never worked for me. I then saw a blog post which showed how to get this to work. Here are the steps for future reference: 


```shell
$ sudo apt remove docker docker-engine docker.io containerd runc
$ sudo apt install apt-transport-https ca-certificates  curl gnupg lsb-release software-properties-common iptables
$ sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
$ /sbin/iptables --version
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$ sudo apt update
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
$ sudo service docker start
$ sudo docker ps -a
$ sudo docker run --rm hello-world
```

Source - https://patrickwu.space/2021/03/09/wsl-solution-to-native-docker-daemon-not-starting/
