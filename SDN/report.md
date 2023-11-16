University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: Principles of designing telecommunication networks  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich    


# Оглавление
- [Упражнение 1](#section1)
- [Упражнение 2](#section2)
- [Упражнение 3](#section3)

## <a name="section1">Упражнение 1</a>
1. Предварительно я скачал официальную виртуальную машину mininet и настроил сеть на "Виртуальный адаптер хоста", чтобы без проблем по ssh подключаться к mininet машине (рисунок 1).  
<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/6d289aa8-b1a4-4412-acb8-3d08e0fcf874"></p>

<p align="center">
  <em>Рисунок 1: Виртуальная машина Mininet с настроенной сетью "Виртуальный адаптер хоста".</em>
</p>

2. Далее запускаем и проверяем установленный пакет mininet (рисунок 2).  
<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/e2210d3a-8920-4ae4-a73f-c32ccc43d5ea" width=400></p>

<p align="center">
  <em>Рисунок 2: Тест Mininet.</em>
</p>

## <a name="section2">Упражнение 2</a>
1. В этом упражнении необходимо создать собственную топологию с использованием mininet. Создаем топологию, используя исходный код скрипта. Она состоит из определенного
числа хостов (от h1 до hN), подключенных к коммутаторам (от s1 до sN). Продемонстритованно на рисунке 3  

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/d062bda3-8712-49c3-986b-cef794c1629a"></p>

<p align="center">
   <em>Рисунок 3: Скрипт линейной топологии.</em> 
</p>

Ping для проверки соединения и iperf для тестирования пропускной способности.

2. Проверка работы LinearTopo представлена на рисунке 4.
<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/21b5477a-ac31-4648-b3eb-8600185d7616"></p>

<p align="center">
  <em>Рисунок 4: Тестирование топологии.</em>
</p>

3. В следующем задании нам необходимо создать простую топологию дерева, изображенную на рисунке 5.  

<p align="center">
<img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/b7bfbe6f-f39d-4d3f-959e-026ed2db2613">
</p>

<p align="center">
  <em>Рисунок 5: Топология дерева.</em> 
</p>

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

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/0c1d3dd1-8832-4112-acfc-750f570c3865"></p>

<p align="center">
  <em>Рисунок 6: Код CustomTopo.py.</em> 
</p>

Результат работы представлен на рисунке 7.

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/28bb872f-10bb-46dd-9058-c4c9d29a1108"></p>

<p align="center">
  <em>Рисунок 7: Вывод CustomTopo.py fanout=2.</em> 
</p>

## <a name="section3">Упражнение 3</a>
1. Сеть, которую мы будем использовать в этом упражнении, включает 3 хоста и коммутатор сконтроллером OpenFlow (POX). Он представлен на рисунке 8.

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/a0586eb7-aca2-49b6-8c67-caaa40991935"></p>

<p align="center">
  <em>Рисунок 8: OpenFlow 3 hosts - 1 switch topology</em> 
</p>

2. POX - это платформа контроллера SDN на базе Python, ориентированная на исследования и образование. Мы должны предварительно отключить контроллер по умолчанию, который использует Mininet во время его моделирования. Убеждаемся, что он не работает в фоновом режиме:

```ps -A | grep controller```
```sudo killall controller```

Для очистки ресурсов Mininet:
```sudo mn -c```

Далее, выполняем команды:
```
sudo mn --topo single,3 --mac --switch ovsk --controller remote

# Контроллер POX поставляется с предустановленным образом VM.
pox.py log.level --DEBUG forwarding.hub
```

На рисунке 9 представлен запуск команды hub.

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/cec901a0-af13-4396-83e5-d9f98a992e7d"></p>

<p align="center">
  <em>Рисунок 9: Запуск примера hub</em> 
</p>

Теперь, при запуске и отмене скрипта запуска контроллера, будет отображаться открытие и закрытие подключения к контроллеру. Например, при запуске команды ```sudo mn --topo single,3 --mac --switch ovsk --controller remote```

<p align="center"><img src="https://github.com/DeFomin/telecom-mininet/assets/90705279/52ce829e-a787-4670-bb9d-675e7055d337"></p>

<p align="center">
  <em>Рисунок 10: Связь контроллера и mininet</em> 
</p>

3. Проверка поведения хаба с помощью tcpdump. Для этого необходимо убедиться, что хосты могут пинговать друг друга и что все узлы видят один и тот же трафик - поведение концентратора. Мы создадим xterms для каждого хоста и просмотрим трафик в каждом.

При этом прищлось решить проблему с подключением к графическому интерфейсу X.












