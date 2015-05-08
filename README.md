#Running Instructions

##Vagrant & VirtualBox
1. Clone this project
2. Install the creativeux/centos7-64-docker Vagrant box (`vagrant box add creativeux/centos7-64-docker`)
3. Pull the creativeux/centos-grunt Docker image (`docker pull creativeux/centos-grunt:latest`)
4. Run `vagrant up` from the root of this project
5. This process will take a while because of the downloads involved.  It will return before the app is running, so if you want to watch the status, you will need to follow the following steps:
  1. `vagrant ssh`
  2. `docker ps` to see the process running in Vagrant.  Copy the process id.
  3. `docker attach {process id}` will tail the output of the process.  To exit, use `Ctrl+p` or `Ctrl+q` to quietly quit.  `Ctrl+c` will kill the process.
  4. When you see the "Waiting..." Grunt output, you are ready for step 6.
6. Open `localhost:9000` in your web browser

##Docker & boot2docker
1. Clone this project
2. Pull the creativeux/centos-grunt Docker image (`docker pull creativeux/centos-grunt:latest`)
3. Get boot2docker running
  1. `boot2docker init` (first time only)
  2. `boot2docker start` (first time & after `boot2docker stop` or reboot)
  3. `boot2docker ip` (record this IP address, it will be where the app will be running)
4. Start the container with all of the appropriate mappings
  1. `docker run -t -i -p 9000:9000 -p 35729:35729 -v $(pwd):/var/www creativeux/centos-grunt` NOTE: This will take a while the first time because `npm install` will be downloading the Internet.  You should see the process in stdout, though.
5. Open `{boot2docker ip}:9000 in your web browser
