# Vagrant tutorial

Your system is referred to as the _host_. 
You will create a virtual machine, with the commands below, which I'll refer to as the _guest_.

Although Vagrant works with both VirtualBox and VMware, 
I assume and Vagrant assumes that you have installed VirtualBox. 

From a terminal on the host, run the following commands. 
```
$ mkdir new_directory; cd new_directory
$ vagrant init
$ ls
```
The second command creates the file `Vagrantfile` in the current directory. 

Now run 
```
echo hello world > say
ls
cat say
```

Now edit `Vagrantfile` with the command
```
$ vi Vagrantfile 
```
and replace “base” with “bento/centos-7.1”. 

Ask vagrant to create the virtual machine from the specifications in `Vagrantfile`, 
which will create a virtual machine running CentOS 7.1. 
```
$ vagrant up 
```
This creates the guest machine called `default` (since we didn't name it). 

Connect to and login to this machine.
```
vagrant ssh default
```

The shell prompt will change to indicate that you are running a shell from within the guest `default`, which you just created. From this shell run
```
ls /vagrant
cat /vagrant/say
```
Notice that the directory `/vagrant` in the guest is synced 
with `new_directory` that you created above (on the host). 

Now run the following
```
exit
```
to stop the shell on the guest and return to the shell on the host. 
Note that the guest is still running. 

To stop the guest run:
```
vagrant halt default
```

This next command won't work as `default` is not running. 
```
vagrant ssh default
```

Run the following to restart the machine. 
```
$ vagrant up 
```

To destroy/delete the guest run:
```
vagrant destroy default
```

Run the following to recreate (and start) the machine. 
```
$ vagrant up 
```

Once the machine is running (up) you can reconnect to it. 
```
vagrant ssh default
```

Exit the shell on the guest:
```
exit
```
Recall, the machine is still running. 