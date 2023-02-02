# Iptables simple examlples

## iptables rules for nfs transparent proxy

Below is an example of nfs transparent proxy via iptables
```
env:
    board ip: 192.168.72.141
    proxy pc with two interfaces, 192.168.72.20, 192.168.17.52
    nfs server: 192.168.17.50
```
It shows the board and the NFS server are not in the same subnet. The board can't mount the nfs server directly
on it. 

Flushing All Rules, Deleting All Chains, and Accepting All
```html linenums="1"
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```
Add NATs for port 111, 2049, 34567(rpc mountd port, manully specified at nfs server side)
```html linenums="1"
iptables -t nat -A PREROUTING -s 192.168.72.141 -p tcp --dport 111 -d 192.168.72.20 -j DNAT --to-destination 192.168.17.50
iptables -t nat -A PREROUTING -s 192.168.72.141 -p tcp --dport 2049 -d 192.168.72.20 -j DNAT --to-destination 192.168.17.50
iptables -t nat -A PREROUTING -s 192.168.72.141 -p tcp --dport 34567 -d 192.168.72.20 -j DNAT --to-destination 192.168.17.50
iptables -t nat -A POSTROUTING -s 192.168.72.141 -d 192.168.17.50 -j SNAT --to-source 192.168.17.52
```


Add FORWARD rules and display iptables rules
```
iptables -t filter -A FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables  -nvL; iptables -t nat -nvL
```

Enable linux kernel ipv4 forward
```
sysctl -w net.ipv4.ip_forward=1
cat /proc/sys/net/ipv4/ip_forward
```

Now run the command below to mount the nfs to local dir '/mnt/nfs'
```
mount -t nfs -o nolock -o tcp 192.168.72.20:/nfs /mnt/nfs
```


Note: In this senario, if the DNATs rules are absent, the proxy pc can work as a router. With the gateway specified to 192.168.72.20, 
the board can communicate with the NFS server directly. Then the mount command should be  
```mount -t nfs -o nolock -o tcp 192.168.17.50:/nfs /mnt/nfs```


iptables persistent rules
```
iptables-save > /etc/iptables/rules.v4
ip6tables-save > /etc/iptables/rules.v6
```


## http transparent redirection
http dowaload proxy for 192.168.17.50
```
iptables -t nat -A PREROUTING -s 192.168.17.50 -p tcp --dport 9817 -j DNAT --to-destination 192.168.0.101:80
iptables -t nat -A POSTROUTING -s 192.168.17.50 -d 192.168.0.101 -j SNAT --to-source 192.168.17.52
```

test url
```
wget http://sdkdown:yiQQ$^*sJ8@192.168.0.101/sdktrack/release?getsdk=FH885XV200_IPC_V1.1.0_20210716
```
