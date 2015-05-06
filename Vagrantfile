Vagrant.configure("2") do |config|

  config.vm.box = "creativeux/centos70-64"
  config.vm.network :forwarded_port, host: 9000, guest: 9000
  config.vm.network :forwarded_port, host: 35729, guest: 35729

  config.vm.synced_folder ".", "/webapp",mount_options: ["dmode=777","fmode=777"]

  # Hack? '--privileged=true' is the only way I was able to get the volumes to map with permissions to run npm installs.
  config.vm.provision "docker" do |d|
      d.pull_images "creativeux/centos-grunt:latest"
      d.run "creativeux/centos-grunt",
        args: "--privileged=true -t -i -p 9000:9000 -p 35729:35729 -v /webapp:/var/www",
        daemonize: true
    end

    config.push.define "atlas" do |push|
      push.app = "creativeux/centos7-64-docker"
    end
end
