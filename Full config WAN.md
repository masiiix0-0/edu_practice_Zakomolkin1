# Отчет по заданию: Full Config Wan

**Выполнил:** Закомолкин М.М.<br>
**Группа:** 9СА-324К

---

## Содержание
[Часть 1. Базовая настройка интерфейсов](#part1)
- [Шаг 1. Построение топологии](#part1-step1)
- [Шаг 2. Настройка R1](#part1-step2)
- [Шаг 3. Настройка R2](#part1-step3)
- [Шаг 4. Настройка R3](#part1-step4)
- [Шаг 5. Настройка R1973](#part1-step5)

[Часть 2. Настройка PPP с аутентификацией CHAP](#part2)
- [Шаг 1. Настройка инкапсуляции PPP на R3 и R1973](#part2-step1)

[Часть 3. Настройка OSPFv2](#part3)
- [Шаг 1. Настройка OSPFv2 на R1, R2, R3](#part3-step1)
- [Шаг 2. Настройка router-id на R2](#part3-step2)
- [Шаг 3. Объявление сетей в OSPF](#part3-step3)
- [Шаг 4. Проверка процесса OSPF](#part3-step4)
- [Шаг 5. Интерфейс f0/0 R1 в area 1](#part3-step5)
- [Шаг 6. Интерфейс f0/1 R1 в area 0](#part3-step6)
- [Шаг 7. Интерфейс f0/0 R2 в area 23](#part3-step7)
- [Шаг 8. Интерфейс f0/1 R2 в area 0](#part3-step8)
- [Шаг 9. Интерфейсы R3 в area 23](#part3-step9)
- [Шаг 10. Блокировка hello-пакетов на R1](#part3-step10)
- [Шаг 11. Настройка R2 как DR](#part3-step11)
- [Шаг 12. Настройка R3 как шлюза по умолчанию](#part3-step12)

[Часть 4. Настройка BGP между R3 и R1973](#part4)
- [Шаг 1-4. Настройка BGP соседства](#part4-step1)
- [Шаг 5. Объявление loopback R1973 в BGP](#part4-step5)
- [Шаг 6. Настройка default route на R1973](#part4-step6)

[Часть 5. Установка лицензий на R3](#part5)
- [Шаг 1. Проверка поддержки лицензий](#part5-step1)
- [Шаг 2. Установка лицензии UCK9](#part5-step2)
- [Шаг 3. Установка лицензии security9](#part5-step3)
- [Шаг 4. Сохранение конфигурации](#part5-step4)

[Часть 6. Настройка DHCP-ретранслятора](#part6)
- [Шаг 1. Настройка R1 как DHCP-ретранслятора](#part6-step1)
- [Шаг 2. Проверка связи](#part6-step2)

[Часть 7. Настройка IPv6-адресов](#part7)
- [Шаг 1. Настройка IPv6 адресов](#part7-step1)
- [Шаг 2. Проверка маршрутизации IPv6](#part7-step2)
- [Шаг 3. Проверка EUI-64 адресации](#part7-step3)

[Часть 8. Настройка OSPFv3](#part8)
- [Шаг 1. Настройка OSPFv3](#part8-step1)
- [Шаг 2. Проверка router-id](#part8-step2)
- [Шаг 3. Проверка объявления сетей](#part8-step3)
- [Шаг 4. Проверка процесса OSPFv3](#part8-step4)
- [Шаг 5. Проверка зон на R1](#part8-step5)
- [Шаг 6. Проверка зон на R2](#part8-step6)
- [Шаг 7. Проверка зон на R3](#part8-step7)
- [Шаг 8. Настройка пассивных интерфейсов на R1](#part8-step8)
- [Шаг 9. Настройка default route на R3](#part8-step9)

[Часть 9. Настройка EIGRPv6](#part9)
- [Шаг 1. Настройка EIGRPv6](#part9-step1)
- [Шаг 2. Проверка AS 100](#part9-step2)
- [Шаг 3. Проверка router-id](#part9-step3)
- [Шаг 4. Анонс loopback R1973 в EIGRPv6](#part9-step4)
- [Шаг 5. Настройка default route на R1973](#part9-step5)

[Полная конфигурация устройств](#part10)

---

# <a id="part1"></a>Часть 1. Базовая настройка интерфейсов

## Цель работы
Настроить базовую IP-адресацию на всех маршрутизаторах в соответствии с заданной топологией сети и обеспечить первичную связность между устройствами.

---

## Задачи
1. Построить топологию сети согласно схеме.
2. Настроить интерфейсы маршрутизатора R1.
3. Настроить интерфейсы маршрутизатора R2.
4. Настроить интерфейсы маршрутизатора R3.
5. Настроить интерфейсы маршрутизатора R1973.

---

## Ход выполнения

### <a id="part1-step1"></a>Шаг 1. Построение топологии
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src=""><img width="2103" height="839" alt="Снимок экрана 2026-03-27 015313" src="https://github.com/user-attachments/assets/4f77f14b-18e7-46c6-a737-7b3c0d538631" />
<br>
  <em>Рисунок 1. Схема топологии сети в Cisco Packet Tracer</em>
</p>

### <a id="part1-step2"></a>Шаг 2. Настройка R1
Настроил R1 в соответствии с ТЗ (техническое задание).
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2c0f6a4e-12ef-4699-825e-3a66fc9037b6"><br>
  <em>Рисунок 2. Настройка R1</em>
</p>

### <a id="part1-step3"></a>Шаг 3. Настройка R2
Настроил R2 в соответствии с ТЗ.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b43dd5cb-3e6d-4d3d-8f9e-4c3a9b6e563c"><br>
  <em>Рисунок 3. Настройка R2</em>
</p>

### <a id="part1-step4"></a>Шаг 4. Настройка R3
Настроил R3 в соответствии с ТЗ.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/1bf671b4-8ebc-4675-8a06-dbc927c13f15"><br>
  <em>Рисунок 4. Настройка R3</em>
</p>

### <a id="part1-step5"></a>Шаг 5. Настройка R1973
Настроил R1973 в соответствии с ТЗ.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/73c3ae47-6532-4b33-aecb-18343c6ee1d6"><br>
  <em>Рисунок 5. Настройка R1973</em>
</p>

---

## Вывод
В первой части работы я построил топологию сети согласно заданию. На всех маршрутизаторах я выполнил базовую настройку интерфейсов с назначением IP-адресов в соответствии с ТЗ.

---

# <a id="part2"></a>Часть 2. Настройка PPP с аутентификацией CHAP

## Цель работы
Настроить последовательное соединение между маршрутизаторами R3 и R1973 с использованием протокола PPP и обеспечить двустороннюю аутентификацию по протоколу CHAP для безопасного обмена данными.

---

## Задачи
1. Изменить инкапсуляцию на последовательных интерфейсах R3 и R1973 на PPP.
2. Создать локальные учетные записи для аутентификации.
3. Настроить аутентификацию CHAP на обоих последовательных интерфейсах.
4. Убедиться, что аутентификация прошла успешно и интерфейсы находятся в состоянии up/up.

---

## Ход выполнения

### <a id="part2-step1"></a>Шаг 1. Настройка инкапсуляции PPP на R3 и R1973
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/979fee27-8035-4900-9c33-6097f31ad757"><br>
  <em>Рисунок 6. Конфигурация на R1973</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e8361301-8fb9-4a5a-9a9e-be38d8ec362b"><br>
  <em>Рисунок 7. Статус интерфейса s0/0/0 на R1973</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/d0c4744a-eed4-44e1-8fbf-4bf22e0ad19f"><br>
  <em>Рисунок 8. Конфигурация на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/9b12420c-a1e4-44b1-93b1-c2a9d0ce8a11"><br>
  <em>Рисунок 9. Статус интерфейса s0/0/0 на R3</em>
</p>

---

## Вывод
Во второй части работы я настроил последовательное соединение между R3 и R1973 с использованием протокола PPP и аутентификации CHAP.

---

# <a id="part3"></a>Часть 3. Настройка OSPFv2

## Цель работы
Настроить протокол динамической маршрутизации OSPFv2 на маршрутизаторах R1, R2 и R3 в соответствии с ТЗ.

---

## Задачи
1. Запустить процесс OSPFv2 на всех трех маршрутизаторах.
2. Установить Router ID 0.0.0.2 на маршрутизаторе R2.
3. Объявить все подключенные сети в OSPF с распределением по зонам.
4. Обеспечить единый номер процесса OSPF 100 на всех маршрутизаторах.
5. Назначить интерфейс f0/0 R1 в зону 1.
6. Назначить интерфейс f0/1 R1 в зону 0.
7. Назначить интерфейс f0/0 R2 в зону 23.
8. Назначить интерфейс f0/1 R2 в зону 0.
9. Назначить интерфейсы g0/0, loopback 3 и loopback 33 R3 в зону 23.
10. Заблокировать отправку hello-пакетов на всех интерфейсах R1, кроме f0/1.
11. Настроить R2 так, чтобы он всегда был назначенным маршрутизатором.
12. Настроить R3 как шлюз по умолчанию.

---

## Ход выполнения

### <a id="part3-step1"></a>Шаг 1. Настройка OSPFv2 на R1, R2, R3
OSPFv2 с номером 100 на каждом маршрутизаторе.
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c9b0a438-2586-4b03-82b1-31f5187dac9e"><br>
  <em>Рисунок 10. Настройка OSPF на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3081782b-b804-4535-b198-d967f3a95e86"><br>
  <em>Рисунок 11. Настройка OSPF на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e650682b-cc4a-4c51-9579-11020e615a99"><br>
  <em>Рисунок 12. Настройка OSPF на R3</em>
</p>

### <a id="part3-step2"></a>Шаг 2. Настройка router-id на R2
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/691d567f-ff72-457a-bdcc-7bd9aaceb2c3"><br>
  <em>Рисунок 12. Настройка router-id на R2</em>
</p>

### <a id="part3-step3"></a>Шаг 3. Объявление сетей в OSPF
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f60bbfff-5408-40af-9210-2b0c44e349dd"><br>
  <em>Рисунок 13. Объявление сетей в зоны 1 и 0 на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b4645433-7fbb-4c0c-a316-baca290349c0"><br>
  <em>Рисунок 14. Объявление сетей в зоны 0 и 23 на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5398d1c7-08ae-4d77-b32e-d81c0ce57e74"><br>
  <em>Рисунок 15. Объявление сетей зоны 23 на R3</em>
</p>

### <a id="part3-step4"></a>Шаг 4. Проверка процесса OSPF
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2128d23e-822b-4de7-8bd8-6d9a405a9e4b"><br>
  <em>Рисунок 16. Проверка OSPF на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/092f6a51-5a8a-447a-bfbb-52e922f7a6b0"><br>
  <em>Рисунок 17. Проверка OSPF на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5916a723-56cb-4da6-b1ec-e9379b6bd2ce"><br>
  <em>Рисунок 18. Проверка OSPF на R3</em>
</p>

### <a id="part3-step5"></a>Шаг 5. Интерфейс f0/0 R1 в area 1
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/97cac656-c8fb-40cc-b22f-5a310074a1eb"><br>
  <em>Рисунок 19. Интерфейс f0/0 R1 в area 1</em>
</p>

### <a id="part3-step6"></a>Шаг 6. Интерфейс f0/1 R1 в area 0
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/56204640-bf87-4276-a614-4b0b22c4610d"><br>
  <em>Рисунок 20. Интерфейс f0/1 R1 в area 0</em>
</p>

### <a id="part3-step7"></a>Шаг 7. Интерфейс f0/0 R2 в area 23
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f2037c5d-68ed-4505-824b-9c86ed19dcc7"><br>
  <em>Рисунок 21. Интерфейс f0/0 R2 в area 23</em>
</p>

### <a id="part3-step8"></a>Шаг 8. Интерфейс f0/1 R2 в area 0
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/83d1305d-6f27-4eac-b1a1-20f7c7b95b25"><br>
  <em>Рисунок 22. Интерфейс f0/1 R2 в area 0</em>
</p>

### <a id="part3-step9"></a>Шаг 9. Интерфейсы R3 в area 23
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/54da57f5-c2a3-4fea-81c2-26dec1ae9e0f"><br>
  <em>Рисунок 23. Интерфейсы R3 в area 23</em>
</p>

### <a id="part3-step10"></a>Шаг 10. Блокировка hello-пакетов на R1
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2b6ec239-3a11-4263-a663-b40f88633233"><br>
  <em>Рисунок 24. Блокировка hello-пакетов на R1</em>
</p>

### <a id="part3-step11"></a>Шаг 11. Настройка R2 как DR
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/0a1a31f2-50e2-4db6-9de6-79a44438cbee"><br>
  <em>Рисунок 25. Настройка R2 как DR</em>
</p>

### <a id="part3-step12"></a>Шаг 12. Настройка R3 как шлюза по умолчанию
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/defd01da-fea9-4816-8c46-56af92e24d7c"><br>
  <em>Рисунок 26. Настройка R3 как шлюза по умолчанию</em>
</p>

---

## Вывод
В третьей части работы я настроил OSPFv2 на R1, R2 и R3 с распределением интерфейсов по зонам 0, 1 и 23. Все соседства установлены, межзональная маршрутизация работает, R3 распространяет маршрут по умолчанию.

---

# <a id="part4"></a>Часть 4. Настройка BGP между R3 и R1973

## Цель работы
Настроить BGP между R3 и R1973.

---

## Задачи
1. Указать номера автономных систем: R3 - AS 3, R1973 - AS 1973.
2. Установить внешнее BGP-соседство между маршрутизаторами.
3. Настроить R1973 на объявление своего loopback-интерфейса R3.
4. Настроить на R1973 маршрут по умолчанию, указывающий на R3.

---

## Ход выполнения

### <a id="part4-step1"></a>Шаг 1-4. Настройка BGP соседства
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/8e4671b6-da92-49e0-a0e2-0c69fd6f9c24"><br>
  <em>Рисунок 27. Настройка BGP на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5bca8a40-7895-4cd0-9d14-7875c8ce4c4d"><br>
  <em>Рисунок 28. Настройка BGP на R1973</em>
</p>

### <a id="part4-step5"></a>Шаг 5. Объявление loopback R1973 в BGP
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f26dda5a-7a36-484f-aef5-81c647e0a3c4"><br>
  <em>Рисунок 29. Объявление сети 73.73.73.0/24 в BGP на R1973</em>
</p>

### <a id="part4-step6"></a>Шаг 6. Настройка default route на R1973
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/665cc726-fa06-4c39-a63f-2e1de35602ac"><br>
  <em>Рисунок 30. Настройка статического маршрута по умолчанию на R1973</em>
</p>

---

## Вывод
В четвёртой части работы я настроил BGP между R3 и R1973. Сессия установлена, сеть 73.73.73.0/24 объявлена в BGP, на R1973 добавлен статический маршрут по умолчанию через R3.

---

# <a id="part5"></a>Часть 5. Установка лицензий на R3

## Цель работы
Установить на маршрутизатор R3 лицензионные пакеты UCK9 и SecurityK9.

---

## Задачи
1. Убедиться, что IOS на R3 поддерживает команды VOIP и расширенные настройки безопасности.
2. Установить лицензию UCK9.
3. Установить лицензию SecurityK9.
4. Сохранить текущую конфигурацию.
5. Перезагрузить маршрутизатор.

---

## Ход выполнения

### <a id="part5-step1"></a>Шаг 1. Проверка поддержки лицензий
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/6bdc319a-5af6-4b8a-804a-9736af3840a9"><br>
  <em>Рисунок 31. Проверка доступных лицензий на R3</em>
</p>

### <a id="part5-step2"></a>Шаг 2. Установка лицензии UCK9
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3e3dc327-feb9-43f2-9117-b67fc5a5e81e"><br>
  <em>Рисунок 32. Команда установки лицензии UCK9</em>
</p>

### <a id="part5-step3"></a>Шаг 3. Установка лицензии security9
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e40f617d-b480-4dba-8d49-a11d5809d963"><br>
  <em>Рисунок 33. Команда установки лицензии securityk9</em>
</p>

### <a id="part5-step4"></a>Шаг 4. Сохранение конфигурации
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/97d3d85b-1af7-49fa-a3b5-9434e3256230"><br>
  <em>Рисунок 34. Сохранение настроек лицензии</em>
</p>

---

## Вывод
В пятой части работы я установил на маршрутизатор R3 лицензионные пакеты UCK9 и SecurityK9. Сначала проверил текущую версию IOS и поддержку лицензий. Затем я добавил лицензии, указав модель маршрутизатора и необходимые технологические пакеты.

---

# <a id="part6"></a>Часть 6. Настройка DHCP-ретранслятора

## Цель работы
Настроить маршрутизатор R1 в качестве DHCP-ретранслятора для обеспечения возможности получения IP-адресов клиенту от DHCP-сервера.

---

## Задачи
1. Настроить на R1 интерфейс f0/0 для перенаправления DHCP-запросов.
2. Настроить DHCP-сервер с пулом адресов для сети 10.1.1.0/24.
3. Проверить связь PC0 с DHCP-сервером.

---

## Ход выполнения

### <a id="part6-step1"></a>Шаг 1. Настройка R1 как DHCP-ретранслятора
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/82442203-ebbf-483a-8ad0-aae4c3e21b7f"><br>
  <em>Рисунок 35. Перенаправление DHCP-запросов на сервер 10.23.23.100</em>
</p>

### <a id="part6-step2"></a>Шаг 2. Проверка связи
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/e07fb77d-9bf3-49d9-8092-10ebb3f35bcf"><br>
  <em>Рисунок 36. Проверка связи PC0 с DHCP-сервером</em>
</p>

---

## Вывод
В шестой части работы я настроил DHCP-ретранслятор на маршрутизаторе R1. На интерфейсе f0/0 обеспечил перенаправление DHCP-запросов от клиента к DHCP-серверу, расположенному в сети 10.23.23.0/24. На Server PT настроил DHCP-пул для сети 10.1.1.0/24. В результате PC0 успешно получил IP-адрес 10.1.1.10 от сервера 10.23.23.100. PC0 пингует DHCP-сервер.

---

# <a id="part7"></a>Часть 7. Настройка IPv6-адресов

## Цель работы
Настроить IPv6-адресацию на всех маршрутизаторах в соответствии с ТЗ, включить маршрутизацию IPv6 и настроить EUI-64 на интерфейсе R1 f0/0.

---

## Задачи
1. Назначить IPv6-адреса всем интерфейсам маршрутизаторов
2. Включить маршрутизацию IPv6 на всех маршрутизаторах.
3. Настроить на интерфейсе f0/0 R1 link-local адрес fe80::1.
4. Настроить на интерфейсе f0/0 R1 глобальный адрес с использованием функции EUI-64.

---

## Ход выполнения

### <a id="part7-step1"></a>Шаг 1. Настройка IPv6 адресов
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b42d304f-423f-41d2-aa5f-573d4ccc20fa"><br>
  <em>Рисунок 37. Настройка IPv6 на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c57b238c-b168-447f-b074-3f7568b50da1"><br>
  <em>Рисунок 38. Настройка IPv6 на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b344e41e-0bb1-4fca-8b17-7f616cb51483"><br>
  <em>Рисунок 39. Настройка IPv6 на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c68b9c2a-e7f3-4703-a085-62a639486d77"><br>
  <em>Рисунок 40. Настройка IPv6 на R1973</em>
</p>

### <a id="part7-step2"></a>Шаг 2. Проверка маршрутизации IPv6
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/317ab19c-25ba-4d6f-908f-8a2762546bc9"><br>
  <em>Рисунок 41. Проверка IPv6-интерфейсов на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/b379b633-d085-408e-b3b5-2e27798cf2cd"><br>
  <em>Рисунок 42. Проверка IPv6-интерфейсов на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2db3bde2-c21d-4bd1-a7b4-9bfc9073d0a1"><br>
  <em>Рисунок 43. Проверка IPv6-интерфейсов на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/4d3326d1-efab-4518-bb4c-a67c832d2f21"><br>
  <em>Рисунок 44. Проверка IPv6-интерфейсов на R1973</em>
</p>

### <a id="part7-step3"></a>Шаг 3. Проверка EUI-64 адресации
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/1cd9be74-3317-491e-a006-19044a0db05f"><br>
  <em>Рисунок 45. Интерфейс f0/0 R1 использует локальный адрес FE80::1</em>
</p>

---

## Вывод
В седьмой части работы я настроил IPv6-адресацию на всех маршрутизаторах. Включил маршрутизацию IPv6 на всех устройствах. Для глобального адреса использовал функцию EUI-64.

---

# <a id="part8"></a>Часть 8. Настройка OSPFv3

## Цель работы
Настроить протокол динамической маршрутизации OSPFv3 для IPv6 на маршрутизаторах R1, R2 и R3.

---

## Задачи
1. Настроить OSPFv3 на R1, R2 и R3 с номером процесса 100.
2. Назначить Router ID: R1 - 0.0.0.1, R2 - 0.0.0.2, R3 - 0.0.0.3.
3. Объявить все подключенные IPv6-сети в OSPFv3.
4. Распределить интерфейсы по зонам.
5. Настроить R1 так, чтобы hello-пакеты отправлялись только через интерфейс f0/1.
6. Настроить R3 как шлюз по умолчанию для всех маршрутизаторов OSPFv3.

---

## Ход выполнения

### <a id="part8-step1"></a>Шаг 1. Настройка OSPFv3
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/701601a6-bedc-4f12-a482-84521c15f8fc"><br>
  <em>Рисунок 46. OSPFv3 на R1 router-id 0.0.0.1 зоны 0 и 1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/c9c953d2-9a5e-42f0-8271-d819f574877a"><br>
  <em>Рисунок 47. OSPFv3 на R2 router-id 0.0.0.2 зоны 0 и 23</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f04e57be-9f6c-4e18-b4e8-ec837f7756ce"><br>
  <em>Рисунок 48. OSPFv3 на R3 router-id 0.0.0.3 зона 23</em>
</p>

### <a id="part8-step2"></a>Шаг 2. Проверка router-id
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/2b45fbcc-1c5c-4e2a-8351-993b8b17d261"><br>
  <em>Рисунок 49. Проверка OSPFv3 R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/0c3f0dc8-9bf3-45a6-91f2-713a3edae075"><br>
  <em>Рисунок 50. Проверка OSPFv3 R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f87c3db0-afc9-400d-a973-021e6cc10250"><br>
  <em>Рисунок 51. Проверка OSPFv3 R3</em>
</p>

### <a id="part8-step3"></a>Шаг 3. Проверка объявления сетей
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/affeeba9-5385-40ee-b1dc-aa09efc61390"><br>
  <em>Рисунок 52. Проверка маршрутов OSPFv3 и интерфейсов на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/5b7a6584-7eea-41ff-a851-b2cddb5137b0"><br>
  <em>Рисунок 53. Проверка маршрутов OSPFv3 и интерфейсов на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/f449c59c-21cc-4805-a4b3-52ebb0218e62"><br>
  <em>Рисунок 54. Проверка маршрутов OSPFv3 и интерфейсов на R3</em>
</p>

### <a id="part8-step4"></a>Шаг 4. Проверка процесса OSPFv3
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/24047078-9d30-478e-ac29-3c1f5f7f85f9"><br>
  <em>Рисунок 55. Процесс OSPFv3 100 на R1</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/cceeeddb-765b-40db-8c04-046ad90a66cd"><br>
  <em>Рисунок 56. Процесс OSPFv3 100 на R2</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/1b49e6ea-d0ef-4a29-bde0-168a2db00847"><br>
  <em>Рисунок 57. Процесс OSPFv3 100 на R3</em>
</p>

### <a id="part8-step5"></a>Шаг 5. Проверка зон на R1
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3d75225b-a095-46f9-b3be-eb1a46c885b0"><br>
  <em>Рисунок 58. Проверка OSPFv3 интерфейсов на R1</em>
</p>

### <a id="part8-step6"></a>Шаг 6. Проверка зон на R2
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/0094c26e-e643-4412-bf7a-4d3410fa530b"><br>
  <em>Рисунок 59. Проверка OSPFv3 интерфейсов на R2</em>
</p>

### <a id="part8-step7"></a>Шаг 7. Проверка зоны на R3
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/316f1de5-c9ab-4bbf-afae-e808f65ce066"><br>
  <em>Рисунок 60. Проверка OSPFv3 интерфейсов на R3</em>
</p>

### <a id="part8-step8"></a>Шаг 8. Настройка пассивных интерфейсов на R1
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/86c79259-0c65-4d3b-8ed4-67d0ec6ef09a"><br>
  <em>Рисунок 61. На R1 блокировка OSPFv3 hello-сообщений на всех интерфейсах кроме f0/1</em>
</p>

### <a id="part8-step9"></a>Шаг 9. Настройка default route на R3
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/3a85aad5-961d-45fd-bec2-322422fb1836"><br>
  <em>Рисунок 62. Настройка распространения маршрута по умолчанию на R3</em>
</p>

---

## Вывод
В восьмой части работы я настроил протокол OSPFv3 для IPv6 на маршрутизаторах R1, R2 и R3 с номером процесса 100. Назначил Router ID для R1 - 0.0.0.1, R2 - 0.0.0.2, R3 - 0.0.0.3. Все интерфейсы объявлены в OSPFv3 с распределением по зонам. Hello-пакеты отправляются только через f0/1 R1. Настроил R3 для работы в качестве шлюза по умолчанию для всех маршрутизаторов OSPF для связи с любыми другими сетями.

---

# <a id="part9"></a>Часть 9. Настройка EIGRPv6

## Цель работы
Настроить протокол динамической маршрутизации EIGRPv6 для IPv6 между маршрутизаторами R3 и R1973.

---

## Задачи
1. Настроить EIGRPv6 на R3 и R1973 с номером автономной системы 100.
2. Назначить Router ID для R3 - 0.0.0.3, R1973 - 0.0.0.73.
3. Настроить R1973 на анонсирование своей loopback-сети в EIGRPv6.
4. Настроить на R1973 маршрут по умолчанию IPv6, указывающий на R3 в качестве next-hop.

---

## Ход выполнения

### <a id="part9-step1"></a>Шаг 1. Настройка EIGRPv6
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/7be4291b-c312-46c5-84ce-f135fcdc3423"><br>
  <em>Рисунок 63. Настройка EIGRPv6 на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/0c9667c2-e67b-4a77-b954-f4f057b1c1bc"><br>
  <em>Рисунок 64. Настройка EIGRPv6 на R1973</em>
</p>

### <a id="part9-step2"></a>Шаг 2. Проверка AS 100

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/ba5b6e55-2489-494d-9c92-f902d42dc31c"><br>
  <em>Рисунок 65. EIGRPv6 AS 100 на R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/65f324f4-ca49-4d04-9928-08b3809db942"><br>
  <em>Рисунок 66. EIGRPv6 AS 100 на R1973</em>
</p>

### <a id="part9-step3"></a>Шаг 3. Проверка router-id
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/a12a676b-0698-439c-b060-e252e1e5a743"><br>
  <em>Рисунок 67. Router-id 0.0.0.3 в конфигурации R3</em>
</p>

<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/305e7e61-b92e-447f-89ff-cb587a275e12"><br>
  <em>Рисунок 68. Router-id 0.0.0.73 в конфигурации R1973</em>
</p>

### <a id="part9-step4"></a>Шаг 4. Анонс loopback R1973 в EIGRPv6
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/67a65a92-eb9d-4dc7-89a2-758e472ddb56"><br>
  <em>Рисунок 69. Включение EIGRPv6 100 на интерфейсе loopback 3</em>
</p>

### <a id="part9-step5"></a>Шаг 5. Настройка default route на R1973
<p align="center">
  <img width="1563" height="671" alt="ч1 1" src="https://github.com/user-attachments/assets/6ac68828-dc17-4834-9424-4ab3cd77fc59"><br>
  <em>Рисунок 70. Статический маршрут по умолчанию на R1973</em>
</p>

---

## Вывод
В девятой части работы я настроил EIGRPv6 между R3 и R1973. Loopback3 R1973 объявлен в EIGRPv6, настроен статический маршрут по умолчанию через R3. Соседство EIGRPv6 установлено, маршрутизация работает.

---

# <a id="part10"></a>Полная конфигурация устройств
<details>
<summary>Конфигурация R1</summary>

```

R1#sh run
Building configuration...

Current configuration : 1134 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
license udi pid CISCO2811/K9 sn FTX1017WUUM-
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
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 10.1.1.1 255.255.255.0
 ip helper-address 10.23.23.100
 duplex auto
 speed auto
 ipv6 address FE80::1 link-local
 ipv6 address 2001:10:10:10::/64 eui-64
 ipv6 ospf 100 area 1
!
interface FastEthernet0/1
 ip address 10.12.12.1 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:11:11:11::1/64
 ipv6 ospf 100 area 0
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 100
 log-adjacency-changes
 passive-interface default
 no passive-interface FastEthernet0/1
 network 10.1.1.0 0.0.0.255 area 1
 network 10.12.12.0 0.0.0.255 area 0
!
ipv6 router ospf 100
 router-id 0.0.0.1
 log-adjacency-changes
 passive-interface default
 no passive-interface FastEthernet0/1
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
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end

```

</details>

<details>
<summary>Конфигурация R2</summary>

```
R2#sh run
Building configuration...

Current configuration : 1002 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R2
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
license udi pid CISCO2811/K9 sn FTX1017PN7N-
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
spanning-tree mode pvst
!
!
!
!
!
!
interface FastEthernet0/0
 ip address 10.23.23.2 255.255.255.0
 ip ospf priority 255
 duplex auto
 speed auto
 ipv6 address 2001:12:12:12::2/64
 ipv6 ospf 100 area 23
!
interface FastEthernet0/1
 ip address 10.12.12.2 255.255.255.0
 ip ospf priority 255
 duplex auto
 speed auto
 ipv6 address 2001:11:11:11::2/64
 ipv6 ospf 100 area 0
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 100
 router-id 0.0.0.2
 log-adjacency-changes
 network 10.12.12.0 0.0.0.255 area 0
 network 10.23.23.0 0.0.0.255 area 23
!
ipv6 router ospf 100
 router-id 0.0.0.2
 log-adjacency-changes
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
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end

```
</details>

<details>
<summary>Конфигурация R3</summary>

```
R3#sh run
Building configuration...

Current configuration : 1671 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R3
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
username R1973 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2911/K9 sn FTX15248JU8-
license boot module c2900 technology-package securityk9
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
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0
 ip address 10.23.23.3 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:12:12:12::3/64
 ipv6 ospf 100 area 23
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/0/0
 ip address 30.30.30.3 255.255.255.0
 encapsulation ppp
 ppp authentication chap
 ipv6 address 2001:30:30:30::3/64
 ipv6 eigrp 100
 clock rate 2000000
!
interface Serial0/0/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 100
 log-adjacency-changes
 network 10.23.23.0 0.0.0.255 area 23
 network 3.0.0.0 0.255.255.255 area 23
 network 33.0.0.0 0.255.255.255 area 23
 default-information originate
!
router bgp 3
 bgp router-id 0.0.0.3
 bgp log-neighbor-changes
 no synchronization
 neighbor 30.30.30.73 remote-as 1973
!
ipv6 router ospf 100
 router-id 0.0.0.3
 default-information originate
 log-adjacency-changes
!
ipv6 router eigrp 100
 eigrp router-id 0.0.0.3
 no shutdown 
!
ip classless
ip route 0.0.0.0 0.0.0.0 Null0 
!
ip flow-export version 9
!
ipv6 route ::/0 2001:12:12:12::2
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end

```
</details>

<details>
<summary>Конфигурация R1937</summary>

```
R1973#sh run
Building configuration...

Current configuration : 1425 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1973
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
username R3 secret 5 $1$mERr$hx5rVt7rPNoS4wqbXKX7m0
!
!
license udi pid CISCO2911/K9 sn FTX1524S832-
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
spanning-tree mode pvst
!
!
!
!
!
!
interface Loopback3
 no ip address
 ipv6 address 2001:1973:1973:1973::1973/64
 ipv6 eigrp 100
!
interface Loopback1973
 ip address 73.73.73.73 255.255.255.0
!
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/0/0
 ip address 30.30.30.73 255.255.255.0
 encapsulation ppp
 ppp authentication chap
 ipv6 address 2001:30:30:30::1973/64
 ipv6 eigrp 100
!
interface Serial0/0/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router bgp 1973
 bgp log-neighbor-changes
 no synchronization
 neighbor 30.30.30.3 remote-as 3
 network 73.73.73.0 mask 255.255.255.0
!
ipv6 router eigrp 100
 eigrp router-id 0.0.0.73
 no shutdown 
!
ip classless
ip route 0.0.0.0 0.0.0.0 30.30.30.3 
!
ip flow-export version 9
!
ipv6 route ::/0 2001:30:30:30::3
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end

```
</details>
