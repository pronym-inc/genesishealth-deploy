# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.synced_folder "src", "/webapps/genesishealth/src"
    config.vm.define "main" do |web|
        web.vm.box = "ubuntu/bionic64"
        web.vm.network "private_network", ip: "192.168.52.50"
        web.vm.provider "virtualbox" do |v|
            v.memory = 2048
        end
        web.vm.provision :ansible_local do |ansible|
            ansible.groups = {
                "all_in_one" => ["main"]
            }
            ansible.playbook = "playbook.yml"
            ansible.tags = "initial"
            ansible.extra_vars = {
                username: "vagrant",
                pronym_environment: "vagrant",
                server_name: "genesishealth.local",
                is_vagrant: true,
                django_app_git_branch: "develop",
                nginx_copy_ssl_certs: false,
                nginx_include_ssl_certs: false,
                nginx_listen_port: 80,
                supervisor_runserver_enabled: true,
                supervisor_gunicorn_enabled: false
            }
        end
    end
end