# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-6.7"
  config.vbguest.auto_update = false
  config.ssh.forward_agent = true
  config.ssh.insert_key = false

  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network :forwarded_port, guest: 8500, host: 8500

  config.vm.provision "shell", inline: <<-EOT
        sudo yum update -y
        # timezone
        cp -p /usr/share/zoneinfo/Japan /etc/localtime
        # iptables off
        /sbin/iptables -F
        /sbin/service iptables stop
        /sbin/chkconfig iptables off
        # Apache
        yum -y install httpd
        /sbin/service httpd restart
        /sbin/chkconfig httpd on
  EOT

  config.vm.provision "shell", path: "install_java.sh"
  config.vm.provision "shell", path: "install_es.sh"

end
