# Атоматическая настройка тестового стенда при помощи Vagrant

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

### Полезные ссылки на ресурсы

<https://www.vagrantup.com> -- официальный сайт Vagrant\
<https://app.vagrantup.com/boxes/search> -- официальный репозиторий box-ов\
<https://github.com/iJackUA/awesome-vagrant> -- много полезного по Vagrant\
<http://vagrant-lists.github.io/> -- большой список plugin-ов\
<https://packer.io> -- создание box-ов\
<https://tinyurl.com/ya97pbys> -- Статья на Хабре по работе с Packer\
<https://github.io/lalbrekht/vagrant/tree/master> -- шаблон Vagrant-файла\
<https://github.com/AnwarYagoub/RHCSA-RHCE-Lab-Environment/blob/master/Vagrantfile>

### Установка и настройка

Vagrant — это простой и удобный в использовании инструмент, позволяющий легко управлять виртуальными машинами из командной строки.\
Vagrant из коробки поддерживает VirtualBox, Hyper-V, Docker, а также имеет возможность управлять другими типами машин, как например VMWare или Amazon EC2, с помощью других так называемых [провайдеров](https://www.vagrantup.com/docs/providers/).\
Стандартные шаблоны виртуальных машин в Vagrant называются боксами. Список общедоступных боксов для Vagrant может быть найден на [странице поиска боксов](https://app.vagrantup.com/boxes/search).

Установка Vagrant в Debian 10:

```
# apt update && apt upgrade
# apt install vagrant
```

Добавление шаблонов:

```
$ vagrant box add debian/buster64
$ vagrant box add centos/7
```

Проверяем список доступных шаблонов:

```
$ vagrant box list
```

Далее создаем директорию, в которой будет храниться наш новый проект:

```
$ mkdir - p ~/develop/vagrant-projects/tutorial
$ cd ~/develop/vagrant-projects/tutorial
```

Далее создаем Vagrant-окружение внутри папки:

```
$ vagrant init debian/buster64
```

Команда vagrant init в текущей директории создает файл Vagrantfile, в котором описывается тип необходимой для проекта машины, каким образом ее сконфигурировать и какие ресурсы выделить.

Запускаем Vagrant-окружение:

```
$ vagrant up
```

Команда vagrant up создает, настраивает и запускает виртуальную машину исходя из параметров заданных в Vagrantfile. При первом запуске она автоматически скачивает необходимый Vagrant-бокс из репозитория и выделяет соответствующие ресурсы для новой виртуальной машины.
