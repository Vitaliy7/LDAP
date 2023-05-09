# LDAP
## Домашнее задание по теме _LDAP. Централизованная авторизация и аутентификация_  
> 1. Установить _FreeIPA_;  
> 2. Написать _Ansible playbook_ для конфигурации клиента;  
> 3. Настроить аутентификацию по SSH-ключам*  

### Выполнение ДЗ.  
1. Сервер разворачивается автоматически, при помощи _Vagrant+Ansible_, но установка собственно сервера _freeipa_ происходит в ручном режиме.  
После выполнения _vagrant_, в той же директории запускаем ```ansible-playbook -i ansible/hosts ansible/server.yml```.  
Эта команда выполнит предварительную настройку и установит _freeipa-server_. Далее подключаемся к серверу и запускаем скрипт установки:
```ipa-server-install```, отвечаем на вопросы установщика, пароль указываем _otus2023_.  
Затем проверим, что сервер Kerberos может выдать нам билет командой ```kinit admin```. На хосте прописываем в _/etc/hosts/_ следующую строку:
_192.168.57.10 ipa.otus.lan_ и с помощью браузера можем открыть страницу управления FreeIPA-сервером по адресу _192.168.57.10_    
Добавлять пользователей можно как через консоль, так и через веб.   
Для добавления пользователя с помощью консоли выполняем:

![](https://github.com/Vitaliy7/LDAP/blob/main/screenshots/2.png?raw=true)  

2. Теперь можно запустить установку клиента: ```ansible-playbook -i ansible/hosts ansible/clients.yml```. После окончания логинимся на  
_client1_ или _client2_ и выполняем:  

![](https://github.com/Vitaliy7/LDAP/blob/main/screenshots/3.png?raw=true)

Процесс добавления хостов к FreeIPA-серверу завершен.  
Веб-консоль администратора FreeIPA с уже добавленным пользователем:  

![](https://github.com/Vitaliy7/LDAP/blob/main/screenshots/4.png?raw=true)