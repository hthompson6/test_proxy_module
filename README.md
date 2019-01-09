# Steps to reproduce
1. On the master server, install the necessary packages:  
`sudo apt-get install salt-api; sudo apt-get install salt-cloud; sudo apt-get install salt-master;
sudo apt-get install salt-ssh; sudo apt-get install salt-syndic`

2. On the proxy minion, install the following packages:
`sudo apt-get install salt-api; sudo apt-get install salt-cloud; sudo apt-get install salt-minion;
sudo apt-get install salt-ssh; sudo apt-get install salt-syndic; sudo apt-get install salt-proxy`

3. On the master server, clone this repository:  
`git clone git@github.com:hthompson6/test_proxy_module.git`

4. Create the salt directory:  
`sudo mkdir /srv/salt`

5. Copy the pillar files over to the srv directory:  
`sudo cp -r ~/test_proxy_module/pillar /srv`

6. Copy the _proxy dir to the salt directory:  
`sudo cp -r ~/test_proxy_module/_proxy /srv/salt`

7. Edit `/etc/salt/proxy` and add an entry for your master's location:  
- `sudo vim /etc/salt/proxy`
- Add `master: <master server ip>` to file

## StackTrace
```[ERROR   ] Proxy Minion failed to start: 
Traceback (most recent call last):
  File "/usr/lib/python2.7/dist-packages/salt/scripts.py", line 192, in proxy_minion_process
    proxyminion.start()
  File "/usr/lib/python2.7/dist-packages/salt/cli/daemons.py", line 486, in start
    self.shutdown()
  File "/usr/lib/python2.7/dist-packages/salt/cli/daemons.py", line 496, in shutdown
    self.minion.opts['proxymodule'][proxy_fn](self.minion.opts)
  File "/usr/lib/python2.7/dist-packages/salt/loader.py", line 900, in __getitem__
    func = super(LazyLoader, self).__getitem__(item)
  File "/usr/lib/python2.7/dist-packages/salt/utils/lazy.py", line 93, in __getitem__
    raise KeyError(key)
KeyError: 'salt.loaded.shutdown'
```

## Enviroment
- Saltstack v2015.8.8
- Ubuntu 16.04

## Architecture
- 1 master server
- 1 proxy minion server
