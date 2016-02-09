# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 8000, host: 8000

  config.vm.synced_folder "repo/", "/tmp/ghp/src/", create: true

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end

  config.ssh.forward_agent = true

  config.vm.provision :shell, :inline => "jekyll serve --source /tmp/ghp/src/ --destination /tmp/ghp/dest/ --force_polling -H 0.0.0.0 -P 8000", run: "always"

end
