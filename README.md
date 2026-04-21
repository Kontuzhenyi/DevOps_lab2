Статический ip
```
sudo nano /etc/netplan/50-cloud-init.yaml
```
Настройка
```
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 10.0.2.15/24
      routes:
        - to: default
          via: 10.0.2.1
      nameservers:
        addresses: [1.1.1.1, 8.8.8.8]
```
Применяем
```
sudo netplan apply
```


Настроен статический ip адрес на двух виртуальных машинах
<img width="853" height="699" alt="image" src="https://github.com/user-attachments/assets/1a7f7264-3c3c-424b-969d-7648169cd20b" />

На второй виртуальной машине создан пользователь без пароля для sudo. Продемонстрировано успешное подключение с первой машины
<img width="837" height="817" alt="image" src="https://github.com/user-attachments/assets/f0f51a4e-f45d-4652-a113-c356da73740b" />

Устанавили ansible на первую виртуальную машину
<img width="926" height="196" alt="image" src="https://github.com/user-attachments/assets/727d2d03-2fb4-4fac-a269-c2ff13599f5e" />

Создаем отдельную папку. В ней мы создадим 3 файла
<img width="332" height="42" alt="image" src="https://github.com/user-attachments/assets/2d949c52-42b1-473b-b195-3acc73982769" />

inventory.ini
```
[webservers]
web1 ansible_host=10.0.2.16 ansible_user=runner
```
index.html
```
<h1>Hello from Ansible</h1>
```
playbook.yml
```
---
- name: Install nginx
  hosts: webservers
  become: true

  tasks:
    - name: Install nginx
      ansible.builtin.apt:
        name: nginx
        update_cache: yes

    - name: Copy index.html
      ansible.builtin.copy:
        src: ./index.html
        dest: /var/www/html/index.html

    - name: Start nginx
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true
```

Проверяем, что ansible работает
<img width="633" height="136" alt="image" src="https://github.com/user-attachments/assets/7ea28ffc-1e2b-4b2b-bcaf-c74adcaea470" />


Продемонстрирован тестовый прогон, но так как я уже сделал боевой, то все тесты будут зелеными
<img width="1279" height="297" alt="image" src="https://github.com/user-attachments/assets/9805677b-a631-4e9e-b016-64caa5c02f4a" />


Делаем боевой прогон и проверяем
<img width="1314" height="828" alt="image" src="https://github.com/user-attachments/assets/888cab44-e7ad-44bc-be4b-de9835d17487" />
