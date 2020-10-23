# SSH Setup on Ubuntu 20.04
Install `openssh-server` (headless images come with this installed):
```bash
sudo apt update
sudo apt install openssh-server
```
Verify the service is running:
```bash
sudo systemctl status ssh

● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-10-22 11:55:14 EDT; 23s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 138773 (sshd)
      Tasks: 1 (limit: 77018)
     Memory: 1.2M
     CGroup: /system.slice/ssh.service
             └─138773 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Oct 22 11:55:14 titan systemd[1]: Starting OpenBSD Secure Shell server...
Oct 22 11:55:14 titan sshd[138773]: Server listening on 0.0.0.0 port 22.
Oct 22 11:55:14 titan sshd[138773]: Server listening on :: port 22.
Oct 22 11:55:14 titan systemd[1]: Started OpenBSD Secure Shell server.
```
And add a rule to the firewall to allow the ssh port to be accessed
```bash
sudo ufw allow ssh
```

## SSH Key Setup
Setting up an ssh key pair is highly recommended due to its increased security benefits and faster connection. Since your system is now exposed to the outside world it is important to have a more rigourous layer of security so malicious users cant just waltz into your kernel.
1. On client machine open a bash terminal and generate an RSA key pair (If you already have an RSA key pair skip this step)
```bash
ssh-keygen -t rsa
```
2. Copy our public RSA key to the server under authorized keys:
```bash
cat ~/.ssh/id_rsa.pub | ssh [username]@[remote_host] "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
3. We are now able to remotely connect to the system using the provided connection specification:
```bash
ssh -p 2022 [username]@[remote_host]
```