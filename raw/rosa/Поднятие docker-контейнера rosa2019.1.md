Поднятие docker-контейнера rosa2019.1

## Поднятие docker-контейнера rosa2019.1

Поднимаем контейнер с abf, abf-c-c и mock для сборки пакетов

1.  Разворачиваем пустой контейнер последнего релиза rosa2019.1:

```
docker run -td --privileged=true -v /home/gel0/omv:/home/omv --name rosa rosalab/rosa2019.1 /bin/bash
```

2.  Входим в шелл контейнера от юзера *omv*, все последующие операции выполняются внутри:

```
sudo docker exec -ti -w /home/omv rosa /bin/bash
```
Если в шеле контейнера не работает Backspace, прописываем это
```
dnf in termcap rootfiles
```
и перезаходим в шелл.

3.  Настраиваем окружение:
    
    - обновляемся
    
    ```
    dnf update && dnf upgrade
    ```
    
    - устанавливаем необходимые пакеты
    
    ```
    dnf install --nogpgcheck -y vim-enhanced sudo rpmdevtools abf-c-c abb basesystem-build git mock termcap rootfiles
    ```
    
    - сетим свои дотфайлы для *root*
    
    ```н
    git clone https://github.com/Gel0bmstu/bashscripts ~/bashscripts &&
    pushd ~/bashscripts ;
    python3 set_dotfiles.py &&
    popd
    . ~/.bashrc
    ```
    
    - добавляем юзера
    
    ```
    useradd omv -G wheel,mock && 
    chown -R omv:omv /home/omv && 
    su - omv
    ```
    
    Сетим дотфайлы и для него.
    
4.  Настраиваем abf:
    
    - запишим в */etc/abf/mock/configs/default.cfg* следующий конфиг: [https://gist.githubusercontent.com/Gel0bmstu/310a0802128773ab8adecde6b3f6ad7a/raw/bf911d310e3a2ff415e677ad1446c7b6428f0e46/abf\_mock\_default.cfg](https://gist.githubusercontent.com/Gel0bmstu/310a0802128773ab8adecde6b3f6ad7a/raw/bf911d310e3a2ff415e677ad1446c7b6428f0e46/abf_mock_default.cfg)
    
    ```
    sudo wget -O /etc/abf/mock/configs/default.cfg https://gist.githubusercontent.com/Gel0bmstu/310a0802128773ab8adecde6b3f6ad7a/raw/bf911d310e3a2ff415e677ad1446c7b6428f0e46/abf_mock_default.cfg
    ```
    
    - запишем в *~/.abfcfg*:  
        [https://gist.githubusercontent.com/Gel0bmstu/94ba5ee26cb29015be5a1f76f94b9668/raw/7c6dbbeeda798ad0fb05ebe2dad26a117f801e81/.abfcfg](https://gist.githubusercontent.com/Gel0bmstu/94ba5ee26cb29015be5a1f76f94b9668/raw/7c6dbbeeda798ad0fb05ebe2dad26a117f801e81/.abfcfg)  
        Здесь необнодимо засетить совои *nickname* и *pass* на abf.
    
    ```
    wget -O ~/.abfcfg https://gist.githubusercontent.com/Gel0bmstu/94ba5ee26cb29015be5a1f76f94b9668/raw/7c6dbbeeda798ad0fb05ebe2dad26a117f801e81/.abfcfg
    ```
    
    - генерим пару ssh ключей и прокидываем через UI на [https://abf.io/settings/ssh_keys](https://abf.io/settings/ssh_keys)
    
    ```
    ssh-keygen && cat ~/.ssh/id_rsa.pub
    ```
5.  Проверяем работу abf:
    

```
mkcd test ;
abf get dos2unix && 
cd dos2unix ;
abf mock -v
```

Для последующего входа в шелл контейнера можно использовать альяс *rce (Rosa Container Enter).*