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

Продемонстрирован тестовый прогон, но так как я уже сделал боевой, то все тесты будут зелеными
<img width="1279" height="297" alt="image" src="https://github.com/user-attachments/assets/9805677b-a631-4e9e-b016-64caa5c02f4a" />


Делаем боевой прогон и проверяем
<img width="1314" height="828" alt="image" src="https://github.com/user-attachments/assets/888cab44-e7ad-44bc-be4b-de9835d17487" />
