# LXC

## Ссылки на ресурсы
- https://gudok.xyz/lxcdeb/

## Установка и настройка
```sh
apt update && apt upgrade

apt install lxc
```




### LXC on deb10
```

apt install lxc libvirt0 libpam-cgfs bridge-utils

# По умолчанию сеть не настроена
#
#
# Список шаблонов
# ls /usr/share/lxc/templates

# Изменить файл /etc/lxc/default.conf
# lxc.net.0.type = veth
# lxc.net.0.link = virbr0
# lxc.net.0.flags = up
# lxc.apparmor.profile = generated
# lxc.apparmor.allow_nesting = 1
```
