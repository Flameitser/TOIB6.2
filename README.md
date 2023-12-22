# Практическое задание №6.2 Настройка протокола GRE

Выполнил студент группы ББМО-02-23 Курченко Иван Дмитриевич

## Общая структурная схема сети
![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/c7971b78-7a9f-4395-b9e3-6f12d9bcbb1c)

# Часть 1

## Шаг 1:  выполните пинг RA с RB.
Используйте команду show ip interface brief на RA, чтобы определить IP-адрес порта S0/0/0.
![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/e56b0747-110a-4d92-9f49-dd94653f7eaf)

С RB выполните пинг IP-адреса 64.103.211.2 на RA.
![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/b5f0a8ad-f264-43cf-b275-0c1b1b59099a)

##  Шаг 2: выполните пинг с PCA на PCB.
![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/4e143177-c8f9-4490-9269-d417e877d5b0)

Пинг не проходит, так как туннель GRE не был настроен

# Часть 2 

## Шаг 1: Настройка туннеля GRE.

Войдите в режим конфигурирования туннеля RA.
    
```

enable

conf t

int tunnel 0

ip address 10.10.10.1 255.255.255.252

tunnel source s0/0/0

tunnel destination 209.165.122.2

tunnel mode gre ip

```

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/5c162a62-13b9-42cd-b3bb-7dcb53bb49d9)




## Шаг 2: Настройте интерфейс Tunnel 0 на RB.

Войдите в режим конфигурирования туннеля RB.
    
```

enable

conf t

int tunnel 0

ip address 10.10.10.2 255.255.255.252

tunnel source s0/0/0

tunnel destination 64.103.211.2

tunnel mode gre ip

```

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/c87175c9-71f0-4739-9419-2ad9d7466d43)


## Шаг 3: Настройка маршрута для частного IP-трафика.

```

conf t

ip route 192.168.2.0 255.255.255.0 10.10.10.2

```
![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/a3a2a12e-cd63-4298-a849-d83532585aef)


```

no shutdown

exit

ip route 192.168.1.0 255.255.255.0 10.10.10.1

```

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/4b883bf6-d5ee-403e-8635-3a43914a7858)


# Часть 3

## Шаг 1: Отправка эхо-запроса с ПК B на ПК А после настройки GRE туннеля

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/4739975e-11f4-43a1-b0d4-edf97b7a5b7a)

## Шаг 2: Сделать трассировку от ПК A до ПК B.

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/d805bafe-8f7b-411c-851b-f9bae54e0f08)


# Проверка правильности выполнения работы

![image](https://github.com/Flameitser/TOIB6.2/assets/65831927/58af59a7-5c0d-4a23-ba69-467c36c94dae)
