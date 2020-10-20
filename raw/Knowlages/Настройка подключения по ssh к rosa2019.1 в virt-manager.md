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