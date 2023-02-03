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

- Which package contains the target file
install *apt-file* and update the cache
```
apt install apt-file
apt-file update
```
search the target file
```
apt-file search /usr/lib32/libstdc++.so.6
```

or use *dpkg* command
```
root@nice-ponies-2:~# dpkg -S libstdc++.so.6
libstdc++6:amd64: /usr/lib/x86_64-linux-gnu/libstdc++.so.6
libstdc++6:amd64: /usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.25
libstdc++6:amd64: /usr/share/gdb/auto-load/usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.25-gdb.py

```
