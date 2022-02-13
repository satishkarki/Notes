# Command Line Butcher

### 1. Killing a process to free a port

**Problem**

I was running my node app in the local host with port 3000.  I didn't not terminate the process. Later, I tried to run a different app on same port and got this error.

```bash
throw er; // Unhandled 'error' event
^
Error: listen EADDRINUSE: address already in use :::3000
```

 **Fix**

```bash
# Print you PID of process bound on that port
fuser 3000/tcp
# Check the application that is using it
htop
# Kill the process
fuser -k 3000/tcp
```

***

### 2. Checking the Ubuntu Version

**Problem**

Sometimes a package can have different configuration for different version of Ubuntu and if you are not sure about which version of Ubuntu you are running then here is a fix

**Fix**

```bash
# Displays all the information
lsb_release -a
```

***

### 3. init System

The init system is the first process started on a Linux platform after the kernel starts, and manages all other processes on the system.

```bash
ps --no-headers -o comm 1
>>> systemd
```

***

### 4. Updating node and npm

**Problem**

I was using an old version of node. I tried to install the mongoose package. It threw the error saying the current mongoose package is not compatible with my node version.

##### [Solution](https://phoenixnap.com/kb/update-node-js-version)

```shell
# First cleared the npm cache
npm cache clean -f
# Installed n, Node's verison manager
sudo npm install -g n
# Installed the latest stable verison
sudo n stable
# Updated the package.json in my app
npm update
```

