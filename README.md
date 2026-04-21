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
