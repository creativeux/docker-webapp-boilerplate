Vagrant.configure("2") do |config|

  config.vm.box = "creativeux/centos7-64-docker"
  config.vm.network :forwarded_port, host: 9000, guest: 9000
  config.vm.network :forwarded_port, host: 35729, guest: 35729

  config.vm.synced_folder ".", "/webapp"

  # Hack? '--privileged=true' is the only way I was able to get the volumes to map with permissions to run npm installs.
  config.vm.provision "docker" do |d|
      d.pull_images "creativeux/centos-grunt:latest"
      d.run "creativeux/centos-grunt",
        args: "--privileged=true -t -i -p 9000:9000 -p 35729:35729 -v /webapp:/var/www",
        daemonize: true
    end
end
