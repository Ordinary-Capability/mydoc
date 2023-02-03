# Common apt usage
- Basic apt commands
```
apt clean all #clean local apt cache
apt update #update package info from apt source
apt install <package>
apt remove <package>
```

- Install package with target version
```
apt install <package>=<version>
```

- Install backported packages
```
apt install <package>/backport-buster
```

- Upgrade
```
apt upgrade #upgrade system packages
apt full-upgrade  #upgrade app packages
```

- Search packages
```
apt list -a <package> #show packages installed and not installed, package name match

apt search <package> #show packages whose name contain the targe string
```
