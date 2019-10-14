Instituto Superior Técnico, Universidade de Lisboa

**Network and Computer Security**

# Lab guide: Traffic Analysis

## Goals

- Gather information about the machines in the network.
- Explore some of the vulnerabilities of TCP / IP.
- Learn about _tcpdump_,_Wireshark,_ _nmap_, _scapy, packit_ _and OpenVAS_ tools.


## Preparation

For this assignment you will need the 2nd and 3rd machines ( **VM2** and **VM3** ) you created in the last assignment. 
You will also need to create a 4th machine (henceforth called **VM4** ) and put it in the same network as machine **VM2** and **VM3** (which was associated to the _Internal Network_). 
Simply cloning **VM3** and changing its static IP to 192.168.1.2 will suffice. 

**It is assumed that VM2 is 192.168.1.254 and VM3 is 192.168.1.1, from the previous laboratory assignment.**


## 1 Listening to the network

We will experiment with three tools: tcpdump, Wireshark and nmap.

### 1.1 tcpdump

The program tcpdump allows you to listen to the local network 
(`$ man tcpdump` for more information).

Run tcpdump in **VM2** and detect the packet ICMP (using ping -c 1) from **VM3** to **VM4**. 
To identify the header, the IP address, the MAC address and protocol use:

```
$ sudo tcpdump -i enp0s8 –X -XX dst host <IP destination>
```

Keep tcpdump running, start a telnet connection between **VM3** and **VM4**. 
Read the username and password of the user. 
Observe that username and password appear letter by letter in different packets (the -i option selects the network interface).

```
$ sudo tcpdump -i enp0s8 –X dst host <IP destination>
```

Keep tcpdump running and start a ssh connection between **VM3** and **VM4**. 
Observe that it is not possible to read the username or password.

You may need to install ssh-server in vm4. To do so execute:

```
$ sudo apt install openssh-server
```

### 1.2 Wireshark

The wireshark program has a similar functionality to that of tcpdump but provides a graphical user interface.

In **VM2** run **wireshark** in command prompt.

```
$ sudo wireshark
```

Go to the **Capture** -\&gt; **Options** menu;
Choose interface **enp0s8** (or the one being used to communicate);
Select: **Update list of packets in real time**, **Automatic scrolling in live capture**, **Hide capture info dialog**.

If you cannot see the save button, just close the Options window. 
Your configurations will be saved.

Click **start a new live capture** ;
Observe the network packets while executing (from **VM3** to **VM4** for example):

```
$ ping
$ telnet
```

See the IP and Ethernet headers.
In the **analyze** menu, do **follow tcp stream** to observe both the username and password.

```
$ ssh
```

Question: Why can you not see the credentials of SSH when using tcpdump or wireshark? 
Try analysing an SSH connection using tcpdump as well.



### 1.3 nmap

The nmap tool provides information from remote machines (`$ man nmap` for more information).

To obtain a list of open ports from a remote machine run:

```
$nmap <IP from remote machine>
```

To obtain the operating system from a remote machine run:

```
$ nmap -O  <IP from remote machine>
```





**Acknowledgments**
...


----

[SIRS Faculty](mailto:meic-sirs@disciplinas.tecnico.ulisboa.pt)

