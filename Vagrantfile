# -*- mode: ruby -*-
# vi: set ft=ruby :

# This script to install Kubernetes will get executed after we have provisioned the box 
$script1 = <<-SCRIPT
# Install kubernetes
"rm /etc/localtime && ln -s /usr/share/zoneinfo/" + timezone + " /etc/localtime", run: "always"
SCRIPT


$script2 = <<-SCRIPT
echo "hi1"
SCRIPT


Vagrant.configure("2") do |config|



config.vm.define "master" do |master|

 require 'time'
  offset = ((Time.zone_offset(Time.now.zone) / 60) / 60)
  timezone_suffix = offset >= 0 ? "+#{offset.to_s}" : "#{offset.to_s}"
  timezone = 'Etc/GMT' + timezone_suffix

master.vm.provider "virtualbox" do |masterconfig|
masterconfig.memory = "3024"
masterconfig.cpus = 3
end


master.vm.box = "geerlingguy/centos7"
master.vm.box_version = "1.2.10"
master.vm.hostname = "kube-master"
master.vm.network "private_network", ip: "172.28.128.3"
master.vm.provision "shell", inline: $script1

end


config.vm.define "worker" do |worker|

worker.vm.provider "virtualbox" do |workerconfig|
workerconfig.memory = "2024"
workerconfig.cpus = 2
end


worker.vm.box = "geerlingguy/centos7"
worker.vm.box_version = "1.2.10"
worker.vm.hostname = "kube-worker"
worker.vm.network "private_network", ip: "172.28.128.4"

worker.vm.provision "shell", inline: $script2

end

end