# Отчет по заданию: Configure LAN

**Выполнил:** Закомолкин М.М.<br>
**Группа:** 9СА-324К

---

## Содержание
[Часть 1. Настройка коммутаторов в Новосибирске](#part1)
- [Шаг 1. Построение топологии](#part1-step1)
- [Шаг 2. Создание сообщения дня](#part1-step2)
- [Шаг 3. Переименование устройств](#part1-step3)
- [Шаг 4. Настройка доменных имен](#part1-step4)
- [Шаг 5. Создание VLAN на коммутаторах в Новосибирске](#part1-step5)
- [Шаг 6. Назначение портов](#part1-step6)
- [Шаг 7. Создание EtherChannel между коммутаторами](#part1-step7)
- [Шаг 8. Создание Management Interface на SW0 для VLAN 1](#part1-step8)
- [Шаг 9. Создание Management Interface на SW1 для VLAN 2](#part1-step9)
- [Шаг 10. Включение SSHv2 на коммутаторах в Новосибирске](#part1-step10)
- [Шаг 11. Настройка транка на интерфейсе f0/24 коммутатора SW0](#part1-step11)
- [Шаг 12. Настройка MOTD для SW0 и SW1](#part1-step12)
- [Шаг 13. Настройка безопасности портов](#part1-step13)
- [Шаг 14. Защита консольного подключения](#part1-step14)
- [Шаг 15. Отключение таймаута exec для консоли и SSH](#part1-step15)
- [Шаг 16. Предотвращение прерывания консольной сессии логами](#part1-step16)
- [Шаг 17. Изменение размера буфера истории](#part1-step17)

[Часть 2. Настройка маршрутизатора R1 и DHCP](#part2)
- [Шаг 1. Назначение IP-адреса интерфейсу f0/1 маршрутизатора R1](#part2-step1)
- [Шаг 2. Настройка маршрутизации между VLAN](#part2-step2)
- [Шаг 3. Настройка DHCP-сервера на R1](#part2-step3)
- [Шаг 4. Проверка связи](#part2-step4)

[Часть 3. Настройка многоуровневого коммутатора MLS](#part3)
- [Шаг 1. Настройка имени хоста](#part3-step1)
- [Шаг 2. Включение возможностей маршрутизации](#part3-step2)
- [Шаг 3. Создание VLAN 100 и 200](#part3-step3)
- [Шаг 4. Назначение интерфейсов в VLAN](#part3-step4)
- [Шаг 5. Включение маршрутизации между VLAN через SVI](#part3-step5)
- [Шаг 6. Настройка интерфейсов 3-го уровня](#part3-step6)
- [Шаг 7. Проверка связи](#part3-step7)

[Часть 4. Настройка HSRP в Москве](#part4)
- [Шаг 1. Настройка IP-адресов на R2](#part4-step1)
- [Шаг 2. Настройка IP-адресов на R3](#part4-step2)
- [Шаг 3. Настройка HSRP](#part4-step3)

[Часть 5. Настройка EIGRP AS 100](#part5)
- [Шаг 1. Настройка EIGRP AS 100 на всех маршрутизаторах и MLS](#part5-step1)
- [Шаг 2. Проверка SSH-подключения с сервера](#part5-step2)
- [Шаг 3. Проверка пинга с сервера](#part5-step3)

[Часть 6. Настройка безопасности (ACL)](#part6)
- [Шаг 1. Настройка ACL на SW2 для управления доступом по VTY](#part6-step1)
- [Шаг 2. Настройка доступа к веб-серверу только для 2.0.0.100](#part6-step2)
- [Шаг 3. Настройка запрета на ответы ping от R2 и R3](#part6-step3)

[Часть 7. Настройка туннеля и RIPv2](#part7)
- [Шаг 1. Создание loopback-интерфейса на R1](#part7-step1)
- [Шаг 2. Создание loopback-интерфейса на R3](#part7-step2)
- [Шаг 3. Настройка RIPv2 на R1 и R3 для объявления loopback-сетей](#part7-step3)
- [Шаг 4. Обеспечение работы RIPv2 только на R1 и R3](#part7-step4)
- [Шаг 5. Настройка GRE-туннеля между R1 и R3](#part7-step5)
- [Шаг 6. Проверка связи между loopback-интерфейсами через туннель](#part7-step6)

[Часть 8. Настройка NTP, Syslog, SNMP, FTP/TFTP](#part8)
- [Шаг 1. Настройка NTP и Syslog](#part8-step1)
- [Шаг 2. Включение SNMP на R2 и R3](#part8-step2)
- [Шаг 3. Включение telnet на R3 с AAA-аутентификацией](#part8-step3)
- [Шаг 4. Настройка R2 на использование FTP-сервера](#part8-step4)
- [Шаг 5. Отправка копии конфигурации R2 на сервер по FTP](#part8-step5)
- [Шаг 6. Отправка копии конфигурации R3 на сервер по TFTP](#part8-step6)
- [Шаг 7. Проверка отсутствия команд boot system на R3](#part8-step7)
- [Шаг 8. Проверка подключения по telnet к R3](#part8-step8)
- [Шаг 9. Изменение локального имени пользователя в R3 с использованием процедур восстановления пароля](#part8-step9)

[Полная конфигурация устройств](#part9)

[Логины и пароли](#part10)

---

# <a id="part1"></a>Часть 1. Настройка коммутаторов в Новосибирске

## Цель работы
Отработать навыки базовой настройки сетевых устройств в Новосибирске.

---

## Задачи
1. Переименовать устройства по шаблону и настроить MOTD-баннеры.
2. На коммутаторах SW0 и SW1 создать VLAN 2–4 и настроить EtherChannel.
3. Организовать безопасное удаленное управление и настроить Management IP.
4. Защитить порты доступа и консоль устройства.

---

## Ход выполнения

### <a id="part1-step1"></a>Шаг 1. Построение топологии
В эмуляторе Cisco Packet Tracer собрал сеть согласно схеме. Топология включает три коммутатора, один многоуровнеый коммутатор и три маршрутизатора, сервер и 8 ПК, соединенные соответствующими интерфейсами.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/21187e6f-3ff9-456b-8c6b-3bee6040daeb"><br>
  <em>Рисунок 1. Схема топологии сети в Cisco Packet Tracer</em>
</p>

### <a id="part1-step2"></a>Шаг 2. Создание сообщения дня
На каждом роутере настроил сообщение дня согласно формату из ТЗ(Техническое задание). На фотографии видно, какую команду я применял.
<p align="center">
 <br>
  <em>Рисунок 2. Настройка MOTD</em>
<image-card alt= src= ></image-card>
### <a id="part1-step3"></a>Шаг 3. Переименование устройств
Переименовал все устройства согласно шаблону ТЗ - как визуально, так и с помощью команды hostname.
<p align="center">
 ![image1](https://github.com/user-attachments/assets/33cd9537-8141-4646-bfbe-b5d1ac83e1bd)

  <em>Рисунок 3. Изменение hostname на rus-nsk-sw0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c4f9cabc-4b82-4cf0-9bf3-8affd3cde236"><br>
  <em>Рисунок 4. Измененные устройства</em>
</p>

### <a id="part1-step4"></a>Шаг 4. Настройка доменных имен
Доменные имена коммутаторов настроил по местоположению.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/522e42e2-d6fe-4331-8f25-f5200dfab792"><br>
  <em>Рисунок 5. Настройка domain-name на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f4e4933a-e5e2-4ec7-8f72-27971311356c"><br>
  <em>Рисунок 6. Настройка domain-name на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/9eece586-bef9-4222-a019-0f141ac0e26c"><br>
  <em>Рисунок 7. Настройка domain-name на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3aa7656e-9fbe-4dca-9035-fe7e7cfaa997"><br>
  <em>Рисунок 8. Настройка domain-name на MLS</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d3f8f3bb-94ab-4cc7-9262-364d15db80b7"><br>
  <em>Рисунок 9. Настройка domain-name на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/759627e5-8654-41f1-ad1f-50daad76be23"><br>
  <em>Рисунок 10. Настройка domain-name на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/25246b69-bdb2-4ee4-a5c0-d17c51b7438c"><br>
  <em>Рисунок 11. Настройка domain-name на SW2</em>
</p>

### <a id="part1-step5"></a>Шаг 5. Создание VLAN на коммутаторах в Новосибирске
На коммутаторах SW0 и SW1 создал VLAN 2, 3 и 4 без присвоения им имен.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/06b9c8cd-66a3-4c3f-99bc-76075f70953a"><br>
  <em>Рисунок 12. Cоздание VLAN на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/9e54b458-57e4-44b0-b624-5b9b6f9b4fdf"><br>
  <em>Рисунок 13. Cоздание VLAN на SW1</em>
</p>

### <a id="part1-step6"></a>Шаг 6. Назначение портов
На коммутаторах SW0 и SW1 выполнил привязку интерфейсов к VLAN согласно нумерации портов.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/8d48a4e5-c608-4870-9677-ab790c860cd9"><br>
  <em>Рисунок 14. Настройка портов для VLAN на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2745d4b3-3f9b-4460-8d56-5bb0e5ae64d5"><br>
  <em>Рисунок 15. Настройка портов для VLAN на SW0</em>
</p>

### <a id="part1-step7"></a>Шаг 7. Создание EtherChannel между коммутаторами
Выполнил настройка EtherChannel между коммутаторами SW0 и SW1. Для агрегации использованы интерфейсы G0/1 и G0/2. На обоих устройствах задал режим active, что обеспечивает инициацию согласования канала с обеих сторон. После создания канала интерфейс Port‑Channel 1 перевел в режим trunk.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/74689d94-4c05-418c-8ae2-813e78d3a132"><br>
  <em>Рисунок 16. EtherChannel на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b1b238f6-d7db-4120-83b4-c838eb4fb940"><br>
  <em>Рисунок 17. EtherChannel на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d83635f5-84f5-4636-84f0-4973d77b1573"><br>
  <em>Рисунок 17.1. EtherChannel на SW0 (продолжение)</em>
</p>

### <a id="part1-step8"></a>Шаг 8. Создание Management Interface на SW0 для VLAN 1
На коммутаторе SW0 выполнил настройку интерфейса управления в VLAN 1. Назначил IP‑адрес 1.0.0.50/8, задал шлюз по умолчанию 1.0.0.1. 
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2d0ca4cd-d0ba-47de-afae-45ffb5f1f124"><br>
  <em>Рисунок 18. Настройка SVI на SW0</em>
</p>

### <a id="part1-step9"></a>Шаг 9. Создание Management Interface на SW1 для VLAN 2
Для SW1 настроил управление через VLAN 2. Задал адрес 2.0.0.50/8 и шлюз 2.0.0.1 - теперь к этому коммутатору тоже можно подключаться удаленно.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/56f29a63-435a-41f7-a3f7-68b1384c7d04"><br>
  <em>Рисунок 19. Настройка SVI на SW1</em>
</p>

### <a id="part1-step10"></a>Шаг 10. Включение SSHv2 на коммутаторах в Новосибирске
Для удаленного управления коммутаторами SW0 и SW1 включил SSHv2. Создал локального пользователя nsk с паролем cisco. Сгенерировал RSA-ключи  настроил VTY-линии  чтобы принимали только SSH-подключения.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e29f38bb-4853-4a15-8e00-e441c21b2426"><br>
  <em>Рисунок 20. Настройка SSHv2 на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5d440b89-ace1-4818-885f-616ce8facd9a"><br>
  <em>Рисунок 21. Настройка SSHv2 на SW0</em>
</p>

### <a id="part1-step11"></a>Шаг 11. Настройка транка на интерфейсе f0/24 коммутатора SW0
Порт f0/24 на SW0, который идет на роутер R1, перевел в режим trunk. Через этот линк будет ходить трафик всех VLAN для маршрутизации между ними.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b4731f41-7cc6-4691-a88f-20583890bb57"><br>
  <em>Рисунок 22. Настройка транка на интерфейсе f0/24 SW0</em>
</p>

### <a id="part1-step12"></a>Шаг 12. Настройка MOTD для SW0 и SW1
Добавил MOTD-баннер на оба коммутатора Новосибирска. На SW0 выводится сообщение «Eto rus-nsk-sw0», на SW1 - «Eto rus-nsk-sw1».
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/15f62d2e-8cb1-4d9b-a37b-77301a4dc654"><br>
  <em>Рисунок 23. Настройка баннера на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/06db7174-304e-48e9-badc-6c2cedec97ce"><br>
  <em>Рисунок 24. Настройка баннера на SW1</em>
</p>

### <a id="part1-step13"></a>Шаг 13. Настройка безопасности портов
Настроил безопасность на портах доступа (f0/2-4) на обоих коммутаторах.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/90ca89f8-1131-4c8f-be30-29f24b1c8214"><br>
  <em>Рисунок 25. Настройка безопасности портов на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f4bf3005-77bf-47f7-9669-974e28d09942"><br>
  <em>Рисунок 25.1. Настройка безопасности портов на SW0 (продолжение)</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/355df864-d939-4390-8943-299366d25731"><br>
  <em>Рисунок 26. Настройка безопасности портов на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/4d7676d2-2dce-47e7-8ffd-2a468cb4cd7d"><br>
  <em>Рисунок 26.1. Настройка безопасности портов на SW1 (продолжение)</em>
</p>

### <a id="part1-step14"></a>Шаг 14. Защита консольного подключения
Настроил защиту консольного подключения на SW0 и SW1. Использовал те же учетные данные, что и для SSH - пользователь nsk с паролем cisco.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/8d63bd8f-6168-4737-993e-23c14e4a333c"><br>
  <em>Рисунок 27. Консольная аутентификация на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/ceb4d743-65bf-48e5-8d84-5f6bd48dbbba"><br>
  <em>Рисунок 28. Консольная аутентификация на SW0</em>
</p>

### <a id="part1-step15"></a>Шаг 15. Отключение таймаута exec для консоли и SSH
Отключил автоматическое завершение сессий по таймауту для консоли и VTY-линий. Теперь сессии не будут разрываться из-за бездействия.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/398cf7d3-aee0-466d-93e7-509ff5e9c375"><br>
  <em>Рисунок 29. Отключение exec-timeout на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5c686680-78c9-465f-b914-198d607f1d18"><br>
  <em>Рисунок 30. Отключение exec-timeout на SW1</em>
</p>

### <a id="part1-step16"></a>Шаг 16. Предотвращение прерывания консольной сессии логами
Настроил синхронизацию логирования на консольной сессии, чтобы системные сообщения не прерывали ввод команд.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/1bf749bd-c0a4-48b3-99b7-9e3ce2068a06"><br>
  <em>Рисунок 31. Синхронизация логирования на SW1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/1b1e1afd-6f0e-42ff-9afb-a21b84dfc279"><br>
  <em>Рисунок 32. Синхронизация логирования на SW0</em>
</p>

### <a id="part1-step17"></a>Шаг 17. Изменение размера буфера истории
Увеличил размер буфера истории команд до 256 строк на консольной сессии и VTY-линиях.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/acaee47f-629d-4ed9-9179-236d5d4e785a"><br>
  <em>Рисунок 33. Настройка размера буфера истории на SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2860bb6c-4185-4fb1-9fc4-567f070c3203"><br>
  <em>Рисунок 34. Настройка размера буфера истории на SW1</em>
</p>

---

## Вывод
1. Все устройства переименовал. Настроил MOTD-баннеры и доменные имена.
2. Создал VLAN 2-4 без имен. Порты доступа f0/2-4 назначил в соответствующие VLAN. Между коммутаторами настроил агрегированный канал EtherChannel с использованием стандартного протокола LACP на интерфейсах G0/1-2. Интерфейс Port-Channel перевел в режим trunk.
3. Настроил Management интерфейсы: VLAN 1 на SW0 и VLAN 2 на SW1 с указанием шлюзов по умолчанию. Включил безопасный доступ по SSHv2, создал учетную запись nsk с паролем cisco. Telnet отключил.
4. На портах доступа применил комплекс мер защиты по ТЗ. 

---

# <a id="part2"></a>Часть 2. Настройка маршрутизатора R1 и DHCP

## Цель работы
Настроить маршрутизатор R1 для обеспечения межсетевой маршрутизации между VLAN и организовать автоматическую раздачу IP-адресов через DHCP-сервер для всех созданных VLAN.

---

## Задачи
1. Назначить IP-адрес интерфейсу f0/1 маршрутизатора R1.
2. Настроить R1 для маршрутизации между VLAN 1-4.
3. Настроить R1 в качестве DHCP-сервера для всех VLAN.
4. Проверить связность сети.

---

## Ход выполнения

### <a id="part2-step1"></a>Шаг 1. Назначение IP-адреса интерфейсу f0/1 маршрутизатора R1
Настроил физический интерфейс f0/1 на роутере R1. Поставил адрес 40.40.40.1/24 - это будет транк-линк, через который пойдёт трафик всех VLAN на коммутатор.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/740b7015-87ff-43e0-8b4a-98a9f6745c74"><br>
  <em>Рисунок 35. Настройка IP-адреса интерфейсу f0/1 на R1</em>
</p>

### <a id="part2-step2"></a>Шаг 2. Настройка маршрутизации между VLAN
Настроил на роутере R1 субинтерфейсы f0/1.1-4 для маршрутизации между VLAN с инкапсуляцией 802.1Q. Каждому субинтерфейсу назначил IP-адрес - шлюз для соответствующей VLAN.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2e618864-4048-4b77-8e95-8add486fff93"><br>
  <em>Рисунок 36. Настройка подинтерфейсов на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/0bb2a5b8-4f35-4b77-829f-78478d78b752"><br>
  <em>Рисунок 36.1. Настройка подинтерфейсов на R1 (продолжение)</em>
</p>

### <a id="part2-step3"></a>Шаг 3. Настройка DHCP-сервера на R1
На маршрутизаторе R1 настроил DHCP-сервер для автоматической раздачи адресов во все VLAN. Создал четыре пула и исключил из диапазонов первые 99 адресов.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/20c38b58-47f8-4002-ace2-f28c2d0853ec"><br>
  <em>Рисунок 37. Создание DHCP пулов на R1</em>
</p>

### <a id="part2-step4"></a>Шаг 4. Проверка связи
Для проверки работоспособности сети и DHCP-сервера выполнил ping с компьютера PC0 (VLAN 2) до адреса 3.0.0.101.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/7dc744ea-faa5-4c64-a7e6-72a711e7a4df"><br>
  <em>Рисунок 38. Проверка связи c PC0</em>
</p>

---

## Вывод
Во второй части работы я настроил маршрутизатор R1 для обеспечения межсетевой маршрутизации между VLAN. Я настроил субинтерфейсы f0/0.1–4 с инкапсуляцией 802.1Q и назначил IP‑адреса шлюзов для каждой VLAN. Кроме того, я настроил R1 в качестве DHCP‑сервера для всех VLAN и проверил связность сети.

---

# <a id="part3"></a>Часть 3. Настройка многоуровневого коммутатора MLS

## Цель работы
Настроить MLS для маршрутизации между VLAN 100 и VLAN 200, а также настроить его интерфейсы 3‑го уровня для подключения к маршрутизаторам.

---

## Задачи
1. Настроить имя хоста и включить IP-маршрутизацию на MLS.
2. Создать VLAN 100 с именем Sales_dept и VLAN 200 с именем IT_dept, назначить порты.
3. Настроить SVI для маршрутизации между VLAN.
4. Настроить интерфейсы 3-го уровня.
5. Проверить связность.

---

## Ход выполнения

### <a id="part3-step1"></a>Шаг 1. Настройка имени хоста
Переименовал многоуровневый коммутатор в rus-msk-mls.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b6e9597e-3ce8-48bd-b79e-a5ef48bf377e"><br>
  <em>Рисунок 39. hostname MLS</em>
</p>

### <a id="part3-step2"></a>Шаг 2. Включение возможностей маршрутизации
На MLS включил IP-маршрутизацию. Теперь коммутатор может пересылать пакеты между разными VLAN без участия внешнего роутера.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/15e9b692-afbd-4a34-8e7c-777ed87c862a"><br>
  <em>Рисунок 40. Включение IP-маршрутизации на MLS</em>
</p>

### <a id="part3-step3"></a>Шаг 3. Создание VLAN 100 и 200
На MLS создал два VLAN с именами для удобства идентификации.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d78371fe-1902-46c6-86b3-005318303633"><br>
  <em>Рисунок 41. Настройка VLAN на MLS</em>
</p>

### <a id="part3-step4"></a>Шаг 4. Назначение интерфейсов в VLAN
Назначил порты на MLS:
1. f0/4 - VLAN 100
2. f0/5 - VLAN 200

Оба порта настроил в режиме access, чтобы подключенные ПК попадали сразу в нужную подсеть.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/009cd417-6b08-4712-9ae9-4706da02759c"><br>
  <em>Рисунок 42. Назначение интерфейсов на MLS</em>
</p>

### <a id="part3-step5"></a>Шаг 5. Включение маршрутизации между VLAN через SVI
Настроил на MLS виртуальные интерфейсы (SVI) для VLAN 100 и 200. Назначил IP-адреса по ТЗ.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/6a0f233f-858a-4211-bfd1-eb0bf7b98fa1"><br>
  <em>Рисунок 43. Настройка SVI для VLAN 100 и 200</em>
</p>

### <a id="part3-step6"></a>Шаг 6. Настройка интерфейсов 3-го уровня
Перевёл порты f0/1-3 на MLS в режим маршрутизируемых портов. Назначил им IP-адреса для связи с другими устройствами.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b168b7b6-c784-493b-b3eb-5d66114bbfe5"><br>
  <em>Рисунок 44. Настройка интерфейсов в режиме 3-го уровня</em>
</p>

### <a id="part3-step7"></a>Шаг 7. Проверка связи
Проверил связность с ПК 6 до адреса 200.0.0.100
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b84c5601-db02-489a-8d67-7502f1e4b496"><br>
  <em>Рисунок 45. Проверка связи</em>
</p>

---

## Вывод
В третьей части работы настроен MLS. Включена IP-маршрутизация, созданы VLAN 100 и 200 с именами и с соответствующими SVI для связи между ними. Интерфейсы f0/1-3 переведены в режим маршрутизируемых портов с назначением IP-адресов для подключения к маршрутизаторам. Проверка пингом подтвердила корректность настроек.

---

# <a id="part4"></a>Часть 4. Настройка HSRP в Москве

## Цель работы
Настроить протокол HSRP(Hot Standby Router Protocol) между R2 и R3 для обеспечения отказоустойчивости шлюза по умолчанию в подсети 10.0.0.0/8.

---

## Задачи
1. Настроить IP-адреса на интерфейсах R2 и R3.
2. Настроить HSRP с виртуальным IP-адресом 10.0.0.1.
3. Сделать R2 активным маршрутизатором, R3 - резервным.
4. Включить вытеснение и отслеживание интерфейса на R2

---

## Ход выполнения

### <a id="part4-step1"></a>Шаг 1. Настройка IP-адресов на R2
На маршрутизаторе R2 настроил IP-адреса на интерфейсах f0/0-1.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b373239c-7f7d-40ab-8529-a7fbd389b398"><br>
  <em>Рисунок 46. Настройка IP-адресов на R2</em>
</p>

### <a id="part4-step2"></a>Шаг 2. Настройка IP-адресов на R3
На маршрутизаторе R3 настроил IP-адреса так же на интерфейсах f0/0-1.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/26466d51-a011-41b5-bfd9-13ec745873ea"><br>
  <em>Рисунок 47. Настройка IP-адресов на R3</em>
</p>

### <a id="part4-step3"></a>Шаг 3. Настройка HSRP
Настроил HSRP на интерфейсе f0/0 обоих маршрутизаторов. Назначил виртуальный IP-адрес 10.0.0.1.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f0db1c9d-cdb2-49ed-adc2-0c93ba476bf9"><br>
  <em>Рисунок 48. Настройка HSRP на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f9715603-14a3-4a41-bb99-23743235a3b6"><br>
  <em>Рисунок 49. Настройка HSRP на R2</em>
</p>

---

## Вывод
В четвёртой части работы настроил протокол HSRP между маршрутизаторами R2 и R3. Виртуальный IP-адрес 10.0.0.1 теперь используется устройствами в сети 10.0.0.0/8 в качестве шлюза по умолчанию. Назначил R2 активным маршрутизатором с приоритетом 110, R3 - резервный с приоритетом 100. Включил вытеснение на обоих маршрутизаторах, а на R2 настроил отслеживание интерфейса F0/1 для автоматического переключения ролей при сбоях.

---

# <a id="part5"></a>Часть 5. Настройка EIGRP AS 100

## Цель работы
Настроить протокол динамической маршрутизации EIGRP с номером автономной системы 100 на всех машрутизаторах и многоуровневом коммутаторе для обеспечения полной связности сети.

---

## Задачи
1. Настроить EIGRP AS 100 на всех устройствах.
2. Анонсировать все подключенные сети.
3. Настроить пассивные интерфейсы.
4. Проверить связность и удаленный доступ.

---

## Ход выполнения

### <a id="part5-step1"></a>Шаг 1. Настройка EIGRP AS 100 на всех маршрутизаторах и MLS
EIGRP AS 100 на R1
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2f163f17-7a34-4eca-ab3c-bf2ed33aaee5"><br>
  <em>Рисунок 50. Конфигурация EIGRP AS 100 на R1</em>
</p>

EIGRP AS 100 на R2
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/02164f47-0a27-42c1-afaa-b88f1683890d"><br>
  <em>Рисунок 51. Конфигурация EIGRP AS 100 на R2</em>
</p>

EIGRP AS 100 на R3
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/74ad4d52-473f-4439-8b38-721efc028489"><br>
  <em>Рисунок 52. Конфигурация EIGRP AS 100 на R3</em>
</p>

EIGRP AS 100 на MLS
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/34dc5b5f-898a-4ced-ad59-7a9e5edcd64f"><br>
  <em>Рисунок 53. Конфигурация EIGRP AS 100 на MLS</em>
</p>

### <a id="part5-step2"></a>Шаг 2. Проверка SSH-подключения с сервера
Проверил удалённый доступ: с сервера подключился по SSH к коммутаторам SW1 и SW2 в Новосибирске. На скриншотах видно успешное подключение.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e23dca45-26a6-4aba-b4c0-58756022bd45"><br>
  <em>Рисунок 54. Подключение по SSH к SW0</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5e523939-cca9-445b-af43-e73972bfa5c9"><br>
  <em>Рисунок 55. Подключение по SSH к SW1</em>
</p>

### <a id="part5-step3"></a>Шаг 3. Проверка пинга с сервера
С сервера выполнил пинг адреса 2.0.0.50 - это управляющий интерфейс коммутатора SW1.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/98c1b990-83d0-4345-8f3a-57f24815ce08"><br>
  <em>Рисунок 56. Проверка связи 10.0.0.100 и 2.0.0.50</em>
</p>

---

## Вывод
В пятой части работы настроил протокол динамической маршрутизации EIGRP AS 100. Все маршрутизаторы и MLS теперь обмениваются маршрутной информацией. Применил стратегию пассивных интерфейсов по умолчанию для повышения безопасности. Проверил связность SSH-подключения.

---

# <a id="part6"></a>Часть 6. Настройка безопасности (ACL)

## Цель работы
Настроить контроль доступа к сетевым устройствам и сервисам с помощью ACL, ограничив SSH-подключения, доступ к веб-серверу и ICMP-трафик для повышения безопасности сети.

---

## Задачи
1. Настроить ACL на SW2 чтобы он принимал SSH-подключения только с сервера и ПК 2.0.0.100.
2. Настроить ACL для разрешения доступа к веб-серверу только с ПК 2.0.0.100
3. Настроить маршрутизацию R2 и R3 так, чтобы они могли инициировать ping к любым устройствам, но не отвечали на входящие запросы ping от других хостов.

---

## Ход выполнения

### <a id="part6-step1"></a>Шаг 1. Настройка ACL на SW2 для управления доступом по VTY
На SW2 создал стандартный ACL 10, который разрешает удаленное управление только с хостов 10.0.0.100 и 2.0.0.100. Затем применил этот список ACL к VTY-линиям, чтобы ограничить доступ.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/345d1766-f813-4066-ba7e-8fa2985ee0db"><br>
  <em>Рисунок 57. Создание ACL 10 на SW2</em>
</p>

### <a id="part6-step2"></a>Шаг 2. Настройка доступа к веб-серверу только для 2.0.0.100
На R1 создал расширенный ACL с именем WEB-ACCESS, который разрешает доступ к веб-серверу только с 2.0.0.100. Весь остальной трафик на веб-сервер блокируется, но другие типы трафика разрешены.

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c0d51086-1390-4c04-9d51-e028272358f3"><br>
  <em>Рисунок 58. Создание расширенного ACL WEB-ACCESS на R1</em>
</p>

### <a id="part6-step3"></a>Шаг 3. Настройка запрета на ответы ping от R2 и R3
На маршрутизаторах R2 и R3 настроил ACL, который позволяет маршрутизаторам пинговать любые устройства, но запрещает отвечать на входящие ping-запросы.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/4e892dc2-e8da-4278-bcd6-a74de61478b1"><br>
  <em>Рисунок 59. Настройка ACL 101 на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/467d56d0-7fe8-4f64-968d-78a5fafe8b82"><br>
  <em>Рисунок 59.1. Настройка ACL 101 на R3 (продолжение)</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c09ca972-f7ae-445e-9a21-bac16fd5f331"><br>
  <em>Рисунок 60. Настройка ACL 101 на R2</em>
</p>

---

## Вывод
1. На SW2 настроен ACl 10, разрешающий удаленное управление только с 10.0.0.100 и 2.0.0.100.
2. На R1 настроен расширенный ACL WEB-ACCESS, который разрешает доступ к веб-серверу только для 2.0.0.100.
3. На R3 и R2 настроен ACL 101, запрещающий отправку ICMP-ответов, что позволяет маршрутизаторам пинговать другие устройства, но не отвечать на внешние запросы.

---

# <a id="part7"></a>Часть 7. Настройка туннеля и RIPv2

## Цель работы
Настроить loopback-интерфейсы на маршрутизаторах R1 и R3, организовать связь между ними через GRE-туннель и настроить RIPv2 только на этих маршрутизаторах.

---

## Задачи
1. Создать loopback-интерфейс 1 на R1 с IP-адресом 192.168.101.1/24.
2. Создать loopback-интерфейс 3 на R3 с IP-адресом 192.168.103.3/24.
3. Настроить RIPv2 на R1 и R3 для объявления loopback-сетей.
4. Обеспечить работу RIPv2 только на R1 и R3.
5. Настроить GRE-туннель между R1 и R3 с адресацией 200.200.200.0/24.
6. Проверить связь между loopback-интерфейсами с помощью расширенного ping.

---

## Ход выполнения

### <a id="part7-step1"></a>Шаг 1. Создание loopback-интерфейса на R1
На маршрутизаторе R1 создал loopback-интерфейс 1 и назначил ему IP-адрес 192.168.101.1/24 согласно заданию. Этот виртуальный интерфейс будет использоваться для тестирования работы GRE-туннеля и протокола RIPv2
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/285f6662-9157-4502-a7eb-21348bea3c22"><br>
  <em>Рисунок 61. Создание loopback-интерфейса на R1</em>
</p>

### <a id="part7-step2"></a>Шаг 2. Создание loopback-интерфейса на R3
Создал на R3 loopback-интерфейс 192.168.103.3/24.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/892e1415-4783-4f42-975d-f4dc455a92b0"><br>
  <em>Рисунок 62. Создание loopback-интерфейса на R3</em>
</p>

### <a id="part7-step3"></a>Шаг 3. Настройка RIPv2 на R1 и R3 для объявления loopback-сетей
Настроил протокол динамической маршрутизации RIPv2 на маршрутизаторах R1 и R3.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/96ebe8d6-ab15-4409-8071-4a46f4cbde40"><br>
  <em>Рисунок 63. Настройка RIPv2 на маршрутизаторе R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/6dfb04a3-38a7-4b46-885f-aba2c140f4cd"><br>
  <em>Рисунок 64. Настройка RIPv2 на маршрутизаторе R1</em>
</p>

### <a id="part7-step4"></a>Шаг 4. Обеспечение работы RIPv2 только на R1 и R3
Сделал так, чтобы RIPv2 работал только на R1 и R3 - настроил passive-interface default, чтобы заблокировать RIP на всех интерфейсах, а затем разрешил его только на fa0/1.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/bdd48cf1-c25f-4a57-b4c4-a4fcca68622e"><br>
  <em>Рисунок 65. RIPv2 только на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/18e32261-9dd4-415b-9614-859ae13ef8f7"><br>
  <em>Рисунок 66. RIPv2 только на R3</em>
</p>

### <a id="part7-step5"></a>Шаг 5. Настройка GRE-туннеля между R1 и R3
Поднял GRE-туннель между R1 и R3: создал интерфейс Tunnel0 с адресом 200.200.200.1/24, указал источник fa0/1 и назначение адрес R3. Добавил сеть туннеля 200.200.200.0 в RIPv2.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c701b279-ac02-45d3-8fc3-3ba36153d1b4"><br>
  <em>Рисунок 67. Настройка GRE-туннеля на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d1c2fb2d-bda8-474c-a8d1-3175967d26fc"><br>
  <em>Рисунок 68. Настройка GRE-туннеля на R3</em>
</p>

### <a id="part7-step6"></a>Шаг 6. Проверка связи между loopback-интерфейсами через туннель
Для проверки связи между loopback-интерфейсами использовал расширенный ping с указанием источника.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f9c362fe-17a6-4127-acd4-841aeffa9585"><br>
  <em>Рисунок 69. Расширенный ping с R1</em>
</p>

---

## Вывод
В седьмой части работы настроил изолированную маршрутизацию между R1 и R3. Создал loopback-интерфейсы, организовал GRE-туннель с адресацией 200.200.200.0/24 и настроил протокол RIPv2 только на этих роутерах. Проверка расширенным ping подтвердила связность между loopback-интерфейсами.

---

# <a id="part8"></a>Часть 8. Настройка NTP, Syslog, SNMP, FTP/TFTP

## Цель работы
Настроить взаимодействие сетевых устройств с сервером 10.0.0.100 для синхронизации времени, централизованного логирования, мониторинга и резервного копирования конфигураций.

---

## Задачи
1. Настроить R1-3 и MLS на использование сервера 10.0.0.100 в качестве защищенного NTP-сервера и Syslog-сервера.
2. Включить SNMP на R2 и R3.
3. Включить telnet на R3 с AAA-аутентификацией через сервер 10.0.0.100.
4. Настроить R2 на использование сервера 10.0.0.100 в качестве FTP-сервера.
5. Отправить копию конфигурации R2 на сервер по FTP.
6. Отправить копию конфигурации R3 на сервер по TFTP.
7. Убедиться, что на R3 нет команд boot system.
8. Проверить возможность подключения к R3 по telnet.
9. Изменить локальное имя пользователя в R3, используя процедуры восстановления пароля.

---

## Ход выполнения

### <a id="part8-step1"></a>Шаг 1. Настройка NTP и Syslog
На R1-3, MLS настроил использование сервера 10.0.0.100 в качестве защищенного NTP-сервера с ключом аутентификации и в качестве Syslog-сервера.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/47ffc789-c2c1-407f-af4c-b65d32fcbcb7"><br>
  <em>Рисунок 70. NTP и Syslog на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/9f91daf4-ffe2-4df4-9672-e617e8ea2736"><br>
  <em>Рисунок 71. NTP и Syslog на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f9886a7d-287b-44e6-bf32-ae1eae3375b5"><br>
  <em>Рисунок 72. NTP и Syslog на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/636d5ac1-7ba3-433b-9d66-71c015bd7d93"><br>
  <em>Рисунок 73. NTP и Syslog на MLS</em>
</p>

### <a id="part8-step2"></a>Шаг 2. Включение SNMP на R2 и R3
На маршрутизаторах R2 и R3 включил SNMP с паролем "cisco" для сообщений set и get.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e64b5f9b-1e16-4151-92e9-9e91a63e1197"><br>
  <em>Рисунок 74. Настройка SNMP на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/87dfb4ea-43da-46af-84fa-7d265f2b6793"><br>
  <em>Рисунок 75. Настройка SNMP на R2</em>
</p>

### <a id="part8-step3"></a>Шаг 3. Включение telnet на R3 с AAA-аутентификацией
Настроил на R3 AAA-аутентификацию для Telnet. Первым делом роутер обращается к серверу 10.0.0.100 для проверки логина и пароля, но если сервер "упал" - используется локальная база пользователь standby.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/86aea75f-0aed-4106-a3e0-6cdbe298e1d9"><br>
  <em>Рисунок 76. Настройка AAA на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/34711c0b-c948-40e4-b524-4e807ad718b7"><br>
  <em>Рисунок 76.1. Настройка AAA на R3 (продолжение)</em>
</p>

### <a id="part8-step4"></a>Шаг 4. Настройка R2 на использование FTP-сервера
На R2 настроил использование сервера 10.0.0.100 в качестве FTP-сервера с учетными данными.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/ff61bd2b-f371-4951-961e-097e207bf700"><br>
  <em>Рисунок 77. Настройка FTP на R2</em>
</p>

### <a id="part8-step5"></a>Шаг 5. Отправка копии конфигурации R2 на сервер по FTP
С R2 отправил копию текущей конфигурации на FTP-сервер 10.0.0.100.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d240c7e5-e550-45b5-97dc-99ee5901c441"><br>
  <em>Рисунок 78. Копирование по FTP с R2</em>
</p>

### <a id="part8-step6"></a>Шаг 6. Отправка копии конфигурации R3 на сервер по TFTP
Сделал бэкап конфигурации R3 на TFTP-сервер 10.0.0.100.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d7bee00b-e95f-4d5e-8740-b6b28470b598"><br>
  <em>Рисунок 79. Копирование по TFTP с R3</em>
</p>

### <a id="part8-step7"></a>Шаг 7. Проверка отсутствия команд boot system на R3
Проверил, что на R3 не используются команды boot system.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/62e53850-1b8d-439d-b696-9e2af31ff7ac"><br>
  <em>Рисунок 80. Проверка boot system</em>
</p>

### <a id="part8-step8"></a>Шаг 8. Проверка подключения по telnet к R3
Проверил возможность подключения к R3 по telnet с маршрутизатора R2, используя имя пользователя standby. Для полного выполнения задания сделал второй вариант, указанный на втором скриншоте.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/713fbb5e-5754-4e25-bf4e-524326cb5f67"><br>
  <em>Рисунок 81. Telnet с R2 к R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3b6f5bea-578c-4b94-bf93-9b372f738b4a"><br>
  <em>Рисунок 82. Ping и Telnet standby</em>
</p>

### <a id="part8-step9"></a>Шаг 9. Изменение локального имени пользователя в R3 с использованием процедур восстановления пароля
На R3 изменил локальное имя пользователя, используя процедуры восстановления пароля.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/45436920-0719-405a-af1a-abb42e622afc"><br>
  <em>Рисунок 83. Процедура восстановления пароля на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b6a1073f-dc2d-45ad-850e-bfd3f3383ede"><br>
  <em>Рисунок 84. Восстановление конфигурации и изменение пароля</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/456fda8c-d326-4094-bfbf-7da1f362cad0"><br>
  <em>Рисунок 85. Завершение настройки пароля и восстановление загрузки</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/7d4992fc-840d-47af-8bc0-9a2f8b3e1c50"><br>
  <em>Рисунок 86. Проверка доступа</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/82d9d2ce-3c43-46bc-ba85-6e3e6920a1d1"><br>
  <em>Рисунок 87. Подтверждение изменения пользователя</em>
</p>

---

## Вывод
В восьмой части работы настроил сервисы управления сетью: NTP и Syslog на устройствах R1-3, MLS с использованием сервера 10.0.0.100, SNMP на R2 и R3, AAA-аутентификацию на R3. Настроил резервное копирование конфигураций через FTP и TFTP. Проверил отсутствие команд boot system на R3, telnet-доступ с именем standby и выполнил процедуру восстановления пароля.




---

# <a id="part9"></a>Полная конфигурация устройств

<details>
<summary>Конфигурация R2 (rus-msk-r2)</summary>

```
rus-msk-r2#sh run
Building configuration...

Current configuration : 1726 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname rus-msk-r2
!
!
!
!
!
!
!
!
no ip cef
no ipv6 cef
!
!
!
username msk privilege 15 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2811/K9 sn FTX10172R10-
!
!
!
!
!
!
!
!
!
ip ftp username cisco
ip ftp password cisco
no ip domain-lookup
ip domain-name msk.local
ip host standby 10.0.0.3 
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 10.0.0.2 255.0.0.0
 ip access-group 101 in
 duplex auto
 speed auto
 standby 1 ip 10.0.0.1
 standby 1 priority 150
 standby 1 preempt
 standby 1 track FastEthernet0/1
!
interface FastEthernet0/1
 ip address 11.0.0.2 255.0.0.0
 ip access-group 101 in
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
router eigrp 100
 network 10.0.0.0
 network 11.0.0.0
 network 40.40.40.0 0.0.0.255
!
ip classless
!
ip flow-export version 9
!
!
access-list 101 permit icmp any any echo-reply
access-list 101 permit icmp host 10.0.0.2 host 10.0.0.3
access-list 101 permit icmp host 10.0.0.3 host 10.0.0.2
access-list 101 permit icmp host 10.0.0.100 any echo
access-list 101 deny icmp any any echo
access-list 101 permit ip any any
!
banner motd ^CRaboty vipolnil Litvinov Ivan Alekseevich student gruppy 9-CA324K, v jyrnale pod nomerom 12 (vrode)^C
!
!
!
snmp-server community cisco RW
!
logging 10.0.0.100
line con 0
 exec-timeout 0 0
 password 7 0822455D0A16
 login
!
line aux 0
!
line vty 0 4
 password 7 0822455D0A16
 login
 transport input telnet
line vty 5 15
 password 7 0822455D0A16
 login
 transport input telnet
!
!
ntp authentication-key 1 md5 0822455D0A16 7
ntp authenticate
ntp trusted-key 1
ntp server 10.0.0.100
!
end
```
</details>

<details>
<summary>Конфигурация SW2 (rus-msk-sw2)</summary>

```
rus-msk-sw2#sh run
Building configuration...

Current configuration : 1267 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-msk-sw2
!
!
!
ip domain-name msk.local
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
!
!
!
access-list 10 permit host 10.0.0.100
access-list 10 permit host 2.0.0.100
line con 0
!
line vty 0 4
 access-class 10 in
 login
 transport input ssh
line vty 5 15
 access-class 10 in
 login
 transport input ssh
!
!
!
!
end
```

</details>

<details>
<summary>Конфигурация R3 (rus-msk-r3)</summary>

```
rus-msk-r3#sh run
Building configuration...

Current configuration : 2324 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-msk-r3
!
!
!
!
!
!
!
aaa new-model
!
aaa authentication login default group tacacs+ local 
aaa authentication login telnet_auth group tacacs+ local 
!
!
!
!
!
!
!
ip cef
no ipv6 cef
!
!
!
username admin privilege 15 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2811/K9 sn FTX1017A65A-
!
!
!
!
!
!
!
!
!
ip domain-name msk.local
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface Loopback3
 ip address 192.168.103.3 255.255.255.0
!
interface Tunnel0
 ip address 200.200.200.3 255.255.255.0
 mtu 1476
 tunnel source FastEthernet0/0
 tunnel destination 40.40.40.1
!
!
interface FastEthernet0/0
 ip address 10.0.0.3 255.0.0.0
 ip access-group 101 in
 duplex auto
 speed auto
 standby 1 ip 10.0.0.1
 standby 1 preempt
!
interface FastEthernet0/1
 ip address 12.0.0.3 255.0.0.0
 ip access-group 101 in
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
router eigrp 100
 network 1.0.0.0
 network 2.0.0.0
 network 3.0.0.0
 network 4.0.0.0
 network 10.0.0.0
 network 11.0.0.0
 network 12.0.0.0
 network 40.40.40.0 0.0.0.255
 network 100.0.0.0
 network 200.0.0.0
!
router rip
 version 2
 passive-interface Vlan1
 passive-interface FastEthernet0/0
 passive-interface FastEthernet0/1
 passive-interface Loopback3
 network 192.168.103.0
 network 200.200.200.0
 no auto-summary
!
ip classless
!
ip flow-export version 9
!
!
access-list 101 permit icmp any any echo-reply
access-list 101 permit icmp host 10.0.0.2 host 10.0.0.3
access-list 101 permit icmp host 10.0.0.3 host 10.0.0.2
access-list 101 permit icmp host 10.0.0.100 any echo
access-list 101 deny icmp any any echo
access-list 101 permit ip any any
!
banner motd ^CRaboty vipolnil Litvinov Ivan Alekseevich student gruppy 9-CA324K, v jyrnale pod nomerom 12 (vrode)^C
!
tacacs-server host 10.0.0.100
tacacs-server key cisco
!
!
snmp-server community cisco RO
!
logging 10.0.0.100
line con 0
!
line aux 0
!
line vty 0 4
 login authentication default
 transport input telnet
 privilege level 15
line vty 5 15
 login authentication default
 transport input telnet
 privilege level 15
!
!
ntp authentication-key 1 md5 0822455D0A16 7
ntp authenticate
ntp trusted-key 1
ntp server 10.0.0.100 key 1
!
end
```

</details>

<details>
<summary>Конфигурация mls (rus-msk-mls)</summary>

```
rus-msk-mls#sh run
Building configuration...

Current configuration : 2371 bytes
!
version 12.2(37)SE1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-msk-mls
!
!
!
ip dhcp excluded-address 200.0.0.1 200.0.0.99
ip dhcp excluded-address 200.0.0.201 200.0.0.254
ip dhcp excluded-address 100.0.0.1 100.0.0.99
ip dhcp excluded-address 100.0.0.201 100.0.0.254
!
ip dhcp pool vlan200
 network 200.0.0.0 255.255.255.0
 default-router 200.0.0.50
ip dhcp pool vlan100
 network 100.0.0.0 255.0.0.0
 default-router 100.0.0.50
!
!
ip routing
!
!
!
!
!
!
!
!
!
!
!
!
!
ip domain-name msk.local
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/1
 no switchport
 ip address 11.0.0.50 255.0.0.0
 duplex auto
 speed auto
!
interface FastEthernet0/2
 no switchport
 ip address 12.0.0.50 255.0.0.0
 duplex auto
 speed auto
!
interface FastEthernet0/3
 no switchport
 ip address 40.40.40.50 255.255.255.0
 duplex auto
 speed auto
!
interface FastEthernet0/4
 switchport access vlan 100
 switchport mode access
!
interface FastEthernet0/5
 switchport access vlan 200
 switchport mode access
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan100
 mac-address 0005.5e97.e901
 ip address 100.0.0.50 255.0.0.0
!
interface Vlan200
 mac-address 0005.5e97.e902
 ip address 200.0.0.50 255.255.255.0
!
router eigrp 100
 network 1.0.0.0
 network 2.0.0.0
 network 3.0.0.0
 network 4.0.0.0
 network 10.0.0.0
 network 11.0.0.0
 network 12.0.0.0
 network 40.40.40.0 0.0.0.255
 network 100.0.0.0
 network 200.0.0.0
 no auto-summary
!
ip classless
!
ip flow-export version 9
!
!
!
!
!
!
!
!
logging 10.0.0.100
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
ntp authentication-key 1 md5 0822455D0A16 7
ntp authenticate
ntp trusted-key 1
ntp server 10.0.0.100 key 1
!
end
```
</details>

<details>
<summary>Конфигурация R1 (rus-nsk-r1)</summary>

```
rus-nsk-r1#sh run
Building configuration...

Current configuration : 2421 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-nsk-r1
!
!
!
!
ip dhcp excluded-address 1.0.0.1 1.0.0.99
ip dhcp excluded-address 2.0.0.1 2.0.0.99
ip dhcp excluded-address 3.0.0.1 3.0.0.99
ip dhcp excluded-address 4.0.0.1 4.0.0.99
!
ip dhcp pool vlan1
 network 1.0.0.0 255.0.0.0
 default-router 1.0.0.1
ip dhcp pool vlan2
 network 2.0.0.0 255.0.0.0
 default-router 2.0.0.1
ip dhcp pool vlan3
 network 3.0.0.0 255.0.0.0
 default-router 3.0.0.1
ip dhcp pool vlan4
 network 4.0.0.0 255.0.0.0
 default-router 4.0.0.1
!
!
!
ip cef
no ipv6 cef
!
!
!
!
license udi pid CISCO2811/K9 sn FTX10171227-
!
!
!
!
!
!
!
!
!
ip domain-name nsk.local
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface Loopback1
 ip address 192.168.101.1 255.255.255.0
!
interface Tunnel0
 ip address 200.200.200.1 255.255.255.0
 mtu 1476
 tunnel source FastEthernet0/1
 tunnel destination 10.0.0.3
!
!
interface FastEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/0.1
 encapsulation dot1Q 1 native
 ip address 1.0.0.1 255.0.0.0
!
interface FastEthernet0/0.2
 encapsulation dot1Q 2
 ip address 2.0.0.1 255.0.0.0
 ip access-group WEB-ACCESS in
!
interface FastEthernet0/0.3
 encapsulation dot1Q 3
 ip address 3.0.0.1 255.0.0.0
!
interface FastEthernet0/0.4
 encapsulation dot1Q 4
 ip address 4.0.0.1 255.0.0.0
!
interface FastEthernet0/1
 ip address 40.40.40.1 255.255.255.0
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
router eigrp 100
 network 1.0.0.0
 network 2.0.0.0
 network 3.0.0.0
 network 4.0.0.0
 network 10.0.0.0
 network 11.0.0.0
 network 12.0.0.0
 network 40.40.40.0 0.0.0.255
 network 100.0.0.0
 network 200.0.0.0
!
router rip
 version 2
 passive-interface FastEthernet0/0
 passive-interface FastEthernet0/1
 passive-interface Loopback1
 network 192.168.101.0
 network 200.200.200.0
 no auto-summary
!
ip classless
!
ip flow-export version 9
!
!
ip access-list extended WEB-ACCESS
 permit tcp host 2.0.0.100 host 10.0.0.100 eq www
 deny tcp any host 10.0.0.100 eq www
 permit ip any any
!
banner motd ^CRaboty vipolnil Litvinov Ivan Alekseevich student gruppy 9-CA324K, v jyrnale pod nomerom 12 (vrode)^C
!
!
!
!
logging 10.0.0.100
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
ntp authentication-key 1 md5 0822455D0A16 7
ntp authenticate
ntp trusted-key 1
ntp server 10.0.0.100 key 1
!
end
```
</details>

<details>
<summary>Конфигурация SW0 (rus-nsk-sw0)</summary>

```
rus-nsk-sw0#sh run
Building configuration...

Current configuration : 2420 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-nsk-sw0
!
!
!
ip ssh version 2
ip domain-name nsk.local
!
username nsk secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface Port-channel1
 switchport mode trunk
!
interface FastEthernet0/1
!
interface FastEthernet0/2
 switchport access vlan 2
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 0001.63DD.83EA
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/3
 switchport access vlan 3
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 0007.EC39.385D
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/4
 switchport access vlan 4
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 000C.8568.18C7
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
 switchport mode trunk
!
interface GigabitEthernet0/1
 switchport mode trunk
 channel-group 1 mode active
!
interface GigabitEthernet0/2
 switchport mode trunk
 channel-group 1 mode active
!
interface Vlan1
 ip address 1.0.0.50 255.0.0.0
!
ip default-gateway 1.0.0.1
!
banner motd ^CEto rus-nsk-sw0^C
!
!
!
line con 0
 logging synchronous
 login local
 history size 256
 exec-timeout 0 0
!
line vty 0 4
 exec-timeout 0 0
 logging synchronous
 login local
 history size 256
 transport input ssh
line vty 5 15
 exec-timeout 0 0
 logging synchronous
 login local
 history size 256
 transport input ssh
!
!
!
!
end
```
</details>

<details>
<summary>Конфигурация SW1 (rus-nsk-sw1)</summary>

```
rus-nsk-sw1#sh run
Building configuration...

Current configuration : 2440 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname rus-nsk-sw1
!
!
!
ip ssh version 2
ip domain-name nsk.local
!
username nsk secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface Port-channel1
 switchport mode trunk
!
interface FastEthernet0/1
!
interface FastEthernet0/2
 switchport access vlan 2
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 0001.C7A0.8514
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/3
 switchport access vlan 3
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 0002.17D3.08D5
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/4
 switchport access vlan 4
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky 
 switchport port-security mac-address sticky 0060.5CDB.4C00
 no cdp enable
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
 switchport mode trunk
 channel-group 1 mode active
!
interface GigabitEthernet0/2
 switchport mode trunk
 channel-group 1 mode active
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan2
 ip address 2.0.0.50 255.0.0.0
!
ip default-gateway 2.0.0.1
!
banner motd ^CEto rus-nsk-sw1^C
!
!
!
line con 0
 logging synchronous
 login local
 history size 256
 exec-timeout 0 0
!
line vty 0 4
 exec-timeout 0 0
 logging synchronous
 login local
 history size 256
 transport input ssh
line vty 5 15
 exec-timeout 0 0
 logging synchronous
 login local
 history size 256
 transport input ssh
!
!
!
!
end
```
</details>

# <a id="part10"></a>Логины и пароли
Username:Password
<details>
<summary>SW1 (rus-nsk-sw1)</summary>

```
nsk:cisco

```
</details>

<details>
<summary>SW0 (rus-nsk-sw0)</summary>

```
nsk:cisco

```

</details>

<details>
<summary>R2 (rus-msk-R2)</summary>

```
-:cisco
```
</details>

<details>
<summary>R3 (rus-msk-R3)</summary>

```
admin:cisco
```
</details>

