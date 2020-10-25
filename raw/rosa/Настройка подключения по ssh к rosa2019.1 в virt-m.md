Настройка подключения по ssh к rosa2019.1 в virt-manager

## Настройка подключения по ssh к rosa2019.1 в virt-manager

Отчищаем файл denyusers, чтобы дать возможность нам коннектиться к машине от любого юзера
```
echo "" | sudo tee /etc/ssh/denyusers > /dev/null
```
Разрешаем коннект от *рута*
```
sudo sed -i "s/\#PermitRootLogin\ prohibit\-password/PermitRootLogin\ yes/g" /etc/ssh/sshd_config
```
сетим пароль для *root*
```
echo 123 | sudo passwd root --stdin
```
рестартим sshd systemd службу
```
sudo systemctl restart sshd
```
далее на хосте чекаем ip адресс развернутой машинки. Здесь *default* - имя бриджа, который проброшен в машинку.
```
virsh net-dhcp-leases default

 Expiry Time           MAC address         Protocol   IP address           Hostname   Client ID or DUID
------------------------------------------------------------------------------------------------------------
 2020-10-21 21:04:14   52:54:00:90:ca:e0   ipv4       192.168.122.240/24   -          01:52:54:00:90:ca:e0

```
подключаемся к машинке
```
ssh root@192.168.122.240
```
---
Скрипт для настройки окружения на новой машине
```
sudo dnf install vim git -y &&
echo "" | sudo tee /etc/ssh/denyusers > /dev/null &&
sudo sed -i "s/\#PermitRootLogin\ prohibit\-password/PermitRootLogin\ yes/g" /etc/ssh/sshd_config && 
echo 123 | sudo passwd root --stdin &&
sudo systemctl restart sshd &&
sudo git clone https://github.com/gel0bmstu/bashscripts /root/bashscripts &&
sudo python3 /root/bashscripts/set_dotfiles.py
```