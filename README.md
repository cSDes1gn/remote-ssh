# Configuring Remote SSH

## Why Remote SSH?
With remote-ssh you can leverage the compute power of your desktop on your laptop from anywhere in the world. Follow this simple setup guide and get access to a headless version of your desktop OS.

## Setup
Before you start, you will need to configure port forwarding on your router. You will need to login to your router to edit the port forwarding rules. This step will be different for different ISPs. The default password for these routers are typically `admin`.

When creating the port forwarding rule be sure to set the following options:
1. Specify the IP of the machine you are allowing remote access to
2. Set the connection type is to `TCP` (or both `TCP` and `UDP` if that is an option)
3. Set the external port address to `2022`
4. Set the internal port to port `22`. This is the well-known port for ssh requests.

Save the rule and visit [this](https://canyouseeme.org) website on the target machine. Enter `2022` for the port number and click *Check Port* to ensure that your ISP is routing the connection properly.

## Quickstart

On the host machine (i.e. the target machine for ssh):

```bash
git clone https://github.com/cSDes1gn/remote-ssh
cd remote-ssh
```
Run the script specifying the external port number you chose in the forwarding rule (here I chose 2022):
```bash
./host-setup 2022
```
This script will yield 2 outputs (highlighted in blue) that are crucial for client configuration:
1. USERNAME
2. IP
Have these on hand for the next step.

On the client machine (i.e. the machine you are connecting with):
```bash
git clone https://github.com/cSDes1gn/remote-ssh
cd remote-ssh
```
Run the script specifying the external port number you chose in the forwarding rule (here I chose 2022), the target system username and the public ip address of the host machine (referenced from the host-setup script):
```bash
./client-setup 2022 christian 64.200.12.32
```

Once complete, disconnect from your router on the client machine and connect to your mobile hotspot or another access point outside your LAN and try connnecting to your host machine:

```bash
ssh -p PORT USERNAME@IP
```