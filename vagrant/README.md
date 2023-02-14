## Атоматическая настройка тестового стенда при помощи Vagrant

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"

  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision "file", source: "~/.ssh/vagrant.pub", destination: "~/.ssh/host.pub"
  config.vm.provision "shell", inline: <<-SHELL
    cat /home/vagrant/.ssh/host.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL

end
```


```sh
# ~/.ssh/config на хост-системе

Host vagrant-vm
        HostName 127.0.0.1
        Port 2222
        User vagrant
        UserKnownHostsFile /dev/null
        StrictHostKeyChecking no
        # PasswordAuthentication no
        IdentityFile "~/.ssh/vagrant"
        IdentitiesOnly yes        
```
