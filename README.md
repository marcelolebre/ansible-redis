# Ansible script for Redis


This ansible script will provision a given VM with a redis listening on all addresses and is booted up automatically at machine start time.

## Steps
### 1) Host configuration
Edit ***hosts*** file and add the ip of the machine to provision.

Example:

```
[target-vm]  
192.168.1.1
```

### 2) Configure user

Edit username on ***install-redis.yml*** file. Depending on your VM setup you may use different users suchs as: ops, admin, root, etc.

Example:

```
remote_user: root
```

### 3) Execute
```
ansible-playbook install-redis.yml -i hosts
```

### Results

If things go accordingly you should see something like this:

```
PLAY [Install Redis] ***********************************************************

TASK [install python2] *********************************************************
ok: [192.168.1.1]

TASK [dependencies : Update ubuntu] ********************************************
ok: [192.168.1.1]

TASK [dependencies : Install build-essentials] *********************************
ok: [192.168.1.1]

TASK [dependencies : Install TCL] **********************************************
ok: [192.168.1.1]

TASK [install : Download Redis] ************************************************
changed: [192.168.1.1]

TASK [install : Unarchive Redis Tar] *******************************************
changed: [192.168.1.1]

TASK [install : build redis] ***************************************************
changed: [192.168.1.1]

TASK [install : testing redis build] *******************************************
changed: [192.168.1.1]

TASK [install : install redis] *************************************************
changed: [192.168.1.1]

TASK [config : create /etc/redis to store redis.conf] **************************
ok: [192.168.1.1]

TASK [config : create /var/lib/redis to store dump files] **********************
ok: [192.168.1.1]

TASK [config : copy redis.conf file] *******************************************
ok: [192.168.1.1]

TASK [config : install redis service] ******************************************
ok: [192.168.1.1]

TASK [config : create redis user] **********************************************
changed: [192.168.1.1]

TASK [config : adjust owner permissions] ***************************************
ok: [192.168.1.1]

TASK [config : limit other users] **********************************************
ok: [192.168.1.1]

TASK [launch : enable redis service] *******************************************
changed: [192.168.1.1]

TASK [launch : restart redis] **************************************************
changed: [192.168.1.1]

TASK [cleanup : cleaning up build files] ***************************************
changed: [192.168.1.1] => (item=redis-stable)
changed: [192.168.1.1] => (item=redis-stable.tar.gz)

PLAY RECAP *********************************************************************
192.168.1.1                 : ok=19   changed=9    unreachable=0    failed=0
```


### Testing
To test that your service is functioning correctly, connect to the Redis server with the command-line client:

```
redis-cli ping
```

If everything is fine, you should receive the following answer:  

```
PONG
```