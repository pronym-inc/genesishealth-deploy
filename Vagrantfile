# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.synced_folder "src", "/webapps/genesishealth/src"
    config.vm.define "web" do |web|
        web.vm.box = "ubuntu/bionic64"
        web.vm.network "private_network", ip: "192.168.52.50"
        web.vm.provider "virtualbox" do |v|
            v.memory = 2048
        end
        web.vm.provision :ansible_local do |ansible|
            ansible.playbook = "playbook.yml"
            ansible.tags = "initial,initial-vagrant"
            ansible.extra_vars = {
                app_username: "vagrant",
                copy_ssl_certs: false,
                django_git_branch: "develop",
                include_ssl_certs: false,
                listen_port: 80,
                nginx_proxy_url: "http://localhost:8000",
                pronym_environment: "vagrant",
                server_name: "genesishealth.local"
            }
        end
    end
end