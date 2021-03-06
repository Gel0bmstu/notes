Поднятие docker-контейнера rosa2019.1

Поднятие docker-контейнера rosa2019.1

## Поднятие docker-контейнера rosa2019.1

Поднимаем контейнер с abf, abf-c-c и mock для сборки пакетов

1.  Разворачиваем пустой контейнер последнего релиза rosa2019.1:

```
docker run -td --privileged=true -v /home/твой_юзер/omv:/home/omv --name rosa rosalab/rosa2019.1
```

2.  Входим в шелл контейнера от юзера *omv*, все последующие операции выполняются внутри:

```
sudo docker exec -ti -u omv rosa /bin/bash
```

3.  Настраиваем окружение:
    
    - обновляемся
    
    ```
    sudo dnf update && sudo dnf upgrade
    ```
    
    - устанавливаем необходимые пакеты
    
    ```
    dnf install --nogpgcheck -y vim-enhanced sudo rpmdevtools abf-c-c abb basesystem-build git
    ```
    
    - сетим свои дотфайлы
    
    ```
    git clone https://github.com/Gel0bmstu/bashscripts ~/bashscripts &&
    cd ~/bashscripts ;
    python3 set_dotfiles.py ;
    . ~/.bashrc
    ```
4.  Настраиваем abf:
    
    - запишим в */etc/abf/mock/configs/default.cfg* следующий конфиг: [https://gist.githubusercontent.com/Gel0bmstu/310a0802128773ab8adecde6b3f6ad7a/raw/bf911d310e3a2ff415e677ad1446c7b6428f0e46/abf\_mock\_default.cfg](https://gist.githubusercontent.com/Gel0bmstu/310a0802128773ab8adecde6b3f6ad7a/raw/bf911d310e3a2ff415e677ad1446c7b6428f0e46/abf_mock_default.cfg)
        
    - запишем в *~/.abfcfg*:  
        [https://gist.githubusercontent.com/Gel0bmstu/94ba5ee26cb29015be5a1f76f94b9668/raw/7c6dbbeeda798ad0fb05ebe2dad26a117f801e81/.abfcfg](https://gist.githubusercontent.com/Gel0bmstu/94ba5ee26cb29015be5a1f76f94b9668/raw/7c6dbbeeda798ad0fb05ebe2dad26a117f801e81/.abfcfg)  
        Здесь необнодимо засетить совои nickname и pass на abf.
        
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

id: 8baed4d9c4d94356bcaef94a1c2ec9f2
parent_id: 184b2c004d544a5184520cce83e42ba5
created_time: 2020-10-19T22:50:00.283Z
updated_time: 2020-10-19T22:50:00.283Z
is_conflict: 0
latitude: 0.00000000
longitude: 0.00000000
altitude: 0.0000
author: 
source_url: 
is_todo: 0
todo_due: 0
todo_completed: 0
source: joplin-desktop
source_application: net.cozic.joplin-desktop
application_data: 
order: 1603147955217
user_created_time: 2020-10-19T22:50:00.283Z
user_updated_time: 2020-10-19T22:50:00.283Z
encryption_cipher_text: 
encryption_applied: 0
markup_language: 1
is_shared: 0
type_: 1