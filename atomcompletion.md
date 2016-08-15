# Generate the docs for jumpscale
```
j.tools.objectinspector.generateDocs(dest='/tmp/tempd', objpath='j.sal')
```
# Generated files in /tmp/tempd
```
In [3]: ls /tmp/tempd/
SUMMARY.md  compl.py  errors.md  jumpscale.api  out.json  sal/
```

# the json api file (out.json)

```
In [4]: cp /tmp/tempd/out.json /opt/salout.json
```

# stubbing json api file 
(https://gist.githubusercontent.com/xmonader/f947f8a48bf208e9a7fe8db547104d02/raw/1b5a59f1d269b4b411adc8da49f78d137e6cf87f/gistfile1.txt)

```
~ > python3 genjs8stub2.py /opt/myjs8xenialopt/salout.json 
Main:  docker
Main:  disklayout
Main:  nettools
Main:  diskmanager
Main:  netconfig
Main:  process
Main:  qemu_img
Main:  ufw
Main:  hostsfile
Main:  fswalker
Main:  cloudfs
Main:  aoe
Main:  fs
Main:  zeronetconfig
Main:  bind
Main:  nic
Main:  nginx
Main:  aysfs
Main:  rsync
Main:  dnsmasq
Main:  ciscoswitch
Main:  tmux
Main:  samba
Main:  unix
Main:  lxc
Main:  routeros
Main:  sshd
Main:  nfs
Main:  btrfs
Main:  ubuntu
Main:  openvswitch

```
# using it from atom
	- go to the settings of autocomplete-python
	- add the path of the completion package for instance ~/compl to `Extra Paths for Packages`
```
import compl.sal as sal


```
I suggest the completion package to be named as JumpScale with each module as a stub
 JumpScale
      - init__.py
      - sal.py
      - data.py
      - application.py
      - ....

so we can use 
``` 
import JumpScale as j
j.sal
```
instead compl.sal

6- I'm facing some issues with metaclasses/objectinspector [j.data.models]
