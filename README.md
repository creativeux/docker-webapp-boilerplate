#Running Instructions
There are two basic ways to run this demo in a Docker container.  You can run the docker container directly on your mac
using boot2docker and VirtualBox, or you can run it in a Vagrant VM that is configured as a Docker daemon.  The Vagrant
approach allows you to run on a Windows box and is the best way to mimic your ci/test/production environments during
development.

##Vagrant & VirtualBox
###Requirements
1. Install Vagrant

###Steps
1. Clone this project
2. Run `vagrant up` from the root of this project
3. This process will take a while because of the downloads involved.  It will return before the app is running, so if you want to watch the status, you will need to follow the following steps:
  1. `vagrant ssh`
  2. `docker ps` to see the process running in Vagrant.  Copy the process id.
  3. `docker attach {process id}` will tail the output of the process.  To exit, use `Ctrl+p` or `Ctrl+q` to quietly quit.  `Ctrl+c` will kill the process.
  4. When you see the "Waiting..." Grunt output, you are ready for step 6.
4. Open `localhost:9000` in your web browser

###Tips
1. You can't just use any base box.  The VM needs to be customized to allow for the Docker daemon to provision.  This includes things like:
  1. Creating a `docker` group and making sure that the `docker` and `vagrant` users are in it
  2. (need to fill this in)
2. When you use `vagrant destroy` you will have to go through the whole Docker image download again because the cache lived in the Vagrant VM.
  1. When you're done working, use `vagrant suspend` to save the state of your environment and `vagrant resume` to bring the environment back.
   
###Todo
1. Parallels provider
2. Restart policy for `vagrant halt` or reboot scenarios 

##boot2docker & VirtualBox
###Requirements
1. Install boot2docker

###Steps
1. Clone this project
2. Get boot2docker running
  1. `boot2docker init` (first time only)
  2. `boot2docker start` (first time & after `boot2docker stop` or reboot)
  3. `boot2docker ip` (record this IP address, it will be where the app will be running)
3. Start the container with all of the appropriate mappings
  1. `docker run --privileged=true -it -p 9000:9000 -p 35729:35729 -v $(pwd):/var/www creativeux/centos-grunt` NOTE: This will take a while the first time because `npm install` will be downloading the Internet.  You should see the process in stdout, though.
4. Open `{boot2docker ip}:9000` in your web browser

###Tips
1. Create an alias in your .bash_profile called `shellinit` (or something) that runs the `$(boot2docker shellinit)` command.  You'll be using that a lot.
