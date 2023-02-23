## LXC
### Содержание
- [Установка и настройка](#setup)
  - [Установка и настройка в Debian 11](#setup_debian11)
- [Использование](#usage)
- [Ссылки на ресурсы](#links)


### Установка и настройка <a name="setup"></a>
#### Установка и настройка в Debian 11 <a name="setup_debian11"></a>

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

### Ссылки на ресурсы
1. [https://gudok.xyz/lxcdeb/](https://gudok.xyz/lxcdeb/)
