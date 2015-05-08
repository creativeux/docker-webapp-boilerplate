#Running Instructions

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
