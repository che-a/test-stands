# -*- mode: ruby -*-
# vim: set ft=ruby :

VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

################################################################################

MASK = "255.255.255.0";
VB_NET = "zbx54-net"

HOSTS = {

    :"zbx54-db" => {
        :box_name => "debian/buster64",
        :cpu => '1',
        :ram => "512",
        :net => [
            {adapter: 2, ip: "192.168.99.10", netmask: MASK, virtualbox__intnet: VB_NET},
        ],
        :port => [
            {guest: 3306, host: 13306},
            {guest: 5432, host: 15432}
        ]
    },

    :"zbx54-srv" => {
        :box_name => "debian/buster64",
        :cpu => '1',
        :ram => "512",
        :net => [
            {adapter: 2, ip: "192.168.99.20", netmask: MASK, virtualbox__intnet: VB_NET},
        ],
        :port => [

        ]
    },

    :"zbx54-web" => {
        :box_name => "debian/buster64",
        :cpu => '2',
        :ram => "768",
        :net => [
            {adapter: 2, ip: "192.168.99.30", netmask: MASK, virtualbox__intnet: VB_NET},
        ],
        :port => [
            {guest: 80, host: 8080},
            {guest: 443, host: 10443}
        ]
    }

}

Vagrant.configure("2") do |config|

    HOSTS.each do |boxname, boxconfig|

        config.vm.define boxname do |box|
=begin
            box.vm.synced_folder ".", "/home/vagrant/sync", type: "virtualbox"
=end
            box.vm.box = boxconfig[:box_name]
            box.vm.host_name = boxname.to_s

            boxconfig[:net].each do |ipconf|
                box.vm.network "private_network", ipconf
            end
            boxconfig[:port].each do |portconf|
                 box.vm.network "forwarded_port", portconf
            end

            box.vm.provider :virtualbox do |vb|
                vb.cpus = boxconfig[:cpu]
                vb.memory = boxconfig[:ram]
                vb.name = "LAB-" + "%s" % boxname
            end
=begin
            box.vm.provision "shell", run: "always", inline: <<-SHELL
                cp -rf /vagrant/files_all_vms/* /
                cp -rf /vagrant/files_individ_vms/* /home/vagrant/
                sed -i 's/NAME=.*/NAME="'$HOSTNAME'"/' /etc/sysconfig/provision.env
                systemctl daemon-reload
                systemctl enable provision.service
                systemctl start provision.service &
            SHELL
=end
        end
    end
end
