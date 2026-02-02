[https://winitpro.ru/index.php/2020/03/17/nastrojka-vlan-interfejsov-v-windows/](https://winitpro.ru/index.php/2020/03/17/nastrojka-vlan-interfejsov-v-windows/)

В зависимости от производителя сетевой карты в несерверных версиях Win vlans прописываются либо с свойствах драйвера либо в фирменных утилитах

## Настройка нескольких VLAN в Windows Server 2016

В Windows Server 2016 можно настроить VLAN с помощью встроенных средств, устанавливать специализированные драйвера или утилиты не нужно. Попробуем настроить несколько разных VLAN на одной физической сетевой карте в Windows Server 2016 с помощью NIC Teaming.

Обязательно убедитесь, что в настройках параметров дополнительных свойств сетевого адаптера не задана VLAN (значение VLAN ID = 0). ![настройка vlanid в свойствах драйвера](https://winitpro.ru/wp-content/uploads/2020/03/nastrojka-vlanid-v-svojstvah-drajvera.png)

1. Запустите **Server Manager** -> **Local** и нажмите на ссылку «**NIC Teaming**«;
2. В секции Teams нажмите **Task** -> **New Team**. Укажите имя группы и выберите сетевые адаптеры, которые нужно в нее добавить;![создать nic teaming интерфейс в windows server 2016](https://winitpro.ru/wp-content/uploads/2020/03/sozdat-nic-teaming-interfejs-v-windows-server-201.png)
3. Можно создать группу NIC Teaming с помощью PowerShell:  
    `New-NetLbfoTeam -Name vTeam -TeamMembers "Ethernet1","Ethernet2" -TeamingMode SwitchIndependent -LoadBalancingAlgorithm Dynamic`
    
4. Теперь в секции «Adapter and Interfaces» можно добавить виртуальные сетевые интерфейсы. Нажмите Tasks -> Add Interface;![Добавить VLAN интерфейс](https://winitpro.ru/wp-content/uploads/2020/03/dobavit-vlan-interfejs.png)
5. Укажите имя создаваемого интерфейса и номер VLAN;![nic teaming добавить vlan в Windows server 2016](https://winitpro.ru/wp-content/uploads/2020/03/nic-teaming-dobavit-vlan-v-windows-server-2016.png)
    
    Из PowerShell добавить сетевой интерфейс и задать ему VLAN можно так:  
    `Add-NetLbfoTeamNic -Team vTeam -VlanID 50 -Name VLAN50`
    
6. Аналогичным образом можно добавить столько сетевых интерфейсов VLAN, сколько нужно;
7. Осталось настроить IP параметры всех созданных виртуальных сетевых интерфейсов в окне **ncpa.cpl.**