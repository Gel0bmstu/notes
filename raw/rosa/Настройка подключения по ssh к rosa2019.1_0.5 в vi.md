Настройка подключения по ssh к rosa2019.1/0.5 в virt-manager

## Настройка подключения по ssh к rosa2019.1 в virt-manager
---
Машинка - ВМ или комп, на котором установлен дистриб росы.
Хост    - комп, с которого мы хотим приконнектиться к Машинке.

--- 
На машинке отчищаем файл denyusers, чтобы дать возможность нам коннектиться к машине от любого юзера
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
рестартим sshd systemd службу.
```
sudo systemctl restart sshd
```
Далее на хосте чекаем ip адресс развернутой машинки. Здесь *default* - имя интерфейса, который машинка используется для похода в сеть.
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
Скрипт для настройки моего окружения на новой машинке
```
echo "" | sudo tee /etc/ssh/denyusers > /dev/null &&
sudo sed -i "s/\#PermitRootLogin\ prohibit\-password/PermitRootLogin\ yes/g" /etc/ssh/sshd_config && 
echo 123 | sudo passwd root --stdin;
if [ $? != 0 ]; then
	echo 1q2w3e4r%T^Y | sudo passwd root --stdin;
fi &&
sudo systemctl restart sshd

dnf install sudo git vim -y &&
git clone https://github.com/gel0bmstu/bashscripts $HOME/bashscripts &&
python3 $HOME/bashscripts/set_dotfiles.py &&
. $HOME/.bashrc
```