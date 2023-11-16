University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: Principles of designing telecommunication networks  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich    

## Упражнение 1
1. Предварительно я скачал официальную виртуальную машину mininet и настроил сеть на "Виртуальный адаптер хоста", чтобы без проблем по ssh подключаться к mininet машине (рисунок 1).  
<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/6d289aa8-b1a4-4412-acb8-3d08e0fcf874">

*Рисунок 1: Виртуальная машина Mininet с настроенной сетью "Виртуальный адаптер хоста".*

2. Далее запускаем и проверяем установленный пакет mininet (рисунок 2).  
<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/e2210d3a-8920-4ae4-a73f-c32ccc43d5ea" width=400>   

*Рисунок 2: Тест mininet.*

## Упражнение 2
1. В этом упражнении необходимо создать собственную топологию с использованием mininet. Создаем топологию, используя исходный код скрипта. Она состоит из определенного
числа хостов (от h1 до hN), подключенных к коммутаторам (от s1 до sN). Продемонстритованно на рисунке 3  

<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/d062bda3-8712-49c3-986b-cef794c1629a">  

*Рисунок 3: Скрипт линейной топологии.*  

Ping для проверки соединения и iperf для тестирования пропускной способности.

2. Проверка работы LinearTopo представлена на рисунке 4.
<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/21b5477a-ac31-4648-b3eb-8600185d7616">

*Рисунок 4: Тестирование топологии.*  

3. В следующем задании нам необходимо создать простую топологию дерева, изображенную на рисунке 5.

<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/b7bfbe6f-f39d-4d3f-959e-026ed2db2613">

*Рисунок 5: Топология дерева.* 

> CustomTopo.py
* skeleton class может поддерживать следующие аргументы:
* linkopts1 : параметр производительности для линков между коммутаторами core и aggregation.
* linkopts2 : параметр производительности для линков между коммутаторами aggregation и edge.
* linkopts3 : параметр производительности для линков между коммутаторами edge и хостом.
* Fanout : параметр fanout означающий число childs per node.
* bw (bandwidth) - пропускная способность
* delay - задержка на связи.

Здесь CustomTopo наследуется от базового класса Topo в Mininet, используется рекурсивный метод __init_tree для создания топологии с заданным уровнем вложенности. В perfTest создается экземпляр топологии и сеть с использованием классов хостов с ограничениями.
Код со значением fanout=2 представлен на рисунке 6.  

<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/0c1d3dd1-8832-4112-acfc-750f570c3865">  

*Рисунок 6: Код CustomTopo.py.* 

Результат работы представлен на рисунке 7.

<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/28bb872f-10bb-46dd-9058-c4c9d29a1108">

*Рисунок 7: Вывод CustomTopo.py fanout=2.* 


