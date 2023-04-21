# -*- mode: ruby -*-
# vi: set ft=ruby :
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # config.vm.box = "nogala/tomcat9"
  # config.vm.box = "generic/centos8"
  # config.vm.box = "generic/rocky8"
  # config.vm.box = "rockylinux/9"
  # config.vm.box = "centos/stream8"
  # config.vm.box = "generic/rhel8"
  # config.vm.box = "generic/rhel7"
  # config.vm.box = "bento/ubuntu-18.04"
  config.vm.box = "generic/ubuntu2004"
  # config.vm.box = “pega-squid/ubuntu-18.04.1-desktop”
  # config.vm.box = "/Users/georgen/Documents/Work/TestDelete/BollyImages/virtualbox-centos8-efi.box"
  # config.vm.box = "/Users/georgen/Documents/Work/TestDelete/BollyImages/virtualbox-rocky8-efi.box"
  # config.vm.box = "generic/centos7"
  # config.vm.box = "mindpointgroup/centos8_apache_base"
  # config.vm.box = "mindpointgroup/cent8_tomcat9_base"
  # config.vm.box = "trueability/esxi-6.7"
  # config.vm.network "private_network", ip: "10.42.0.50"
  # Windows 10 Below
  # config.vm.network "private_network", ip: "192.168.56.2"
  # config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  # config.vm.synced_folder "/Users/georgen/Documents/Work/ControlWork/STIG", "/var/tmp", type: "virtualbox"
  # config.ssh.username = 'vagrant'
  # config.ssh.password = 'vagrant'
  # config.vm.provider "virtualbox" do |hw|
  #   hw.memory = 4096
  #   hw.cpus = 2
  # end
  config.vm.provision "ansible" do |ansible|
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/STIG/tomcat-stig/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/STIG/POSTGRES-9-STIG/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/STIG/Oracle-7/RHEL7-STIG/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/STIG/TOMCAT-9-STIG/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/CIS/rhel-8/site.yaml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/STIG/rhel-8-stig/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/CIS/apache-cis/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/CIS/APACHE-2.4-CIS/site.yml"
    # ansible.playbook = "playbook_rhel8_stig.yml"
    # ansible.playbook = "playbook_rhel8_stig.yml"
    # ansible.playbook = "./test_playbook/site.yml"
    # ansible.playbook = "update_upgrade.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ClientWork/CBS/1045/RHEL7-CIS/site.yaml"
    # ansible.playbook = "/Users/stephenw/Documents/Development/RHEL7-STIG/site.yml"
    # ansible.playbook = "/Users/stephenw/Documents/Development/Testing (Ok If Deleted)/RHEL9-CIS/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/ControlWork/temp/RHEL8-STIG-TEST/site.yml"
    # ansible.playbook = "/Users/stephenw/Documents/Development/Testing (Ok If Deleted)/UBUNTU18-STIG/site.yml"
    # ansible.playbook = "/Users/stephenw/Documents/Development/Testing (Complete)/UBUNTU20-STIG/site.yml"
    # ansible.playbook = "/Users/georgen/Documents/Work/TempDelete/pr_233_staging/RHEL7-CIS/site.yml"
    ansible.playbook = "/Users/stephenw/Documents/Development/UBUNTU20-CIS/site.yml"
    ansible.verbose = "vvvvv"
  end
end
