Vagrant.configure("2") do |config|

  ###
  ### NOTE!!!
  ###
  ### Due to a Vagrant race condition between
  ### "setting hostname through Vagrant"
  ### and "systemctl restart network.service"
  ### no hostnames will be set using Vagrant.
  ### This will have to be done through Ansible afterwards!

   config.vm.define "tyk_01" do |tyk_01|
     tyk_01.vm.synced_folder "./vagrant", "/vagrant"
     tyk_01.vm.box = "generic/oracle7"
     tyk_01.vm.network :"private_network", ip: "172.28.129.201", auto_config: true
     tyk_01.vm.network "forwarded_port", guest: 3000, host: 3000, protocol: "tcp"
     tyk_01.vm.network "forwarded_port", guest: 8081, host: 8081, protocol: "tcp"
     tyk_01.vm.provider :virtualbox do |v|
       v.customize ["modifyvm", :id, "--memory", 1024]
       v.customize ["modifyvm", :id, "--cpus", "2"]
       v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
       v.customize ["modifyvm", :id, "--usb", "off"]
       v.customize ["modifyvm", :id, "--audio", "none"]
       v.customize ["modifyvm", :id, "--name", "tyk_01"]
     end # End of "tyk_01.vm.provider"
   end   # End of config.vm.define "tyk_01"

   config.vm.define "keycloak_01" do |keycloak_01|
     keycloak_01.vm.synced_folder "./vagrant", "/vagrant"
     keycloak_01.vm.box = "generic/oracle7"
     keycloak_01.vm.network :"private_network", ip: "172.28.129.202", auto_config: true
     keycloak_01.vm.network "forwarded_port", guest: 8080, host: 8080, protocol: "tcp"
     keycloak_01.vm.provider :virtualbox do |v|
       v.customize ["modifyvm", :id, "--memory", 1024]
       v.customize ["modifyvm", :id, "--cpus", "2"]
       v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
       v.customize ["modifyvm", :id, "--usb", "off"]
       v.customize ["modifyvm", :id, "--audio", "none"]
       v.customize ["modifyvm", :id, "--name", "keycloak_01"]
     end # End of "keycloak_01.vm.provider"
   end   # End of config.vm.define "keycloak_01"

   config.vm.define "httpd_01" do |httpd_01|
     httpd_01.vm.synced_folder "./vagrant", "/vagrant"
     httpd_01.vm.box = "generic/oracle7"
     httpd_01.vm.network :"private_network", ip: "172.28.129.203", auto_config: true
     httpd_01.vm.network "forwarded_port", guest: 80, host: 80, protocol: "tcp"
     httpd_01.vm.provider :virtualbox do |v|
       v.customize ["modifyvm", :id, "--memory", 1024]
       v.customize ["modifyvm", :id, "--cpus", "2"]
       v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
       v.customize ["modifyvm", :id, "--usb", "off"]
       v.customize ["modifyvm", :id, "--audio", "none"]
       v.customize ["modifyvm", :id, "--name", "httpd_01"]
     end # End of "httpd_01.vm.provider"
   end   # End of config.vm.define "httpd_01"
end       # End of "Vagrant.configure"
