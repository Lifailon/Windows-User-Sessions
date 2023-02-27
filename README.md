# Windows-User-Sessions
Шаблон для проверки кол-ва активных и неактивных терминальных сессий и списка пользователей на машинах с ОС Windows. Протестирвоано на Windows Server 2016-2019 и Windows 10.

![Image alt](https://github.com/Lifailon/Windows-User-Sessions/blob/rsa/Screen/Windows.jpg)

![Image alt](https://github.com/Lifailon/Windows-User-Sessions/blob/rsa/Screen/Zabbix.jpg)

### Настройка.
1. Импортируйте шаблон **[Windows-User-Sessions](https://github.com/Lifailon/Windows-User-Sessions/tree/rsa/Template)** в Zabbix.

2. На клиентской машине с Zabbix Agent:
* Задать в zabbix_agentd.conf параметр Include, в котором будет содержаться путь к файлу конфигурации:
`Include=.\zabbix_agent2.d\plugins.d\*.conf`
* Поместить **[User-Sessions.conf](https://github.com/Lifailon/Windows-User-Sessions/blob/rsa/Scripts/User-Sessions.conf)** с пользовательскими параметрами (UserParamete) в каталог, путь к которому указан в zabbix_agentd.conf
* Поместить каталог User-Sessions с содержимым **[Get-Query-Param.ps1 ](https://github.com/Lifailon/Windows-User-Sessions/blob/rsa/Scripts/User-Sessions/Get-Query-Param.ps1)** в каталог, путь к которому указан в User-Sessions.conf. Скрипт содержим модуль **[Get-Query](https://github.com/Lifailon/Get-Query)** и пользовательские параметры, которые он принимает от Zabbix.
* Разрешить выполнение незарегистрированных сценариев PowerShell: Set-ExecutionPolicy Unrestricted -Force
* Перезапустить службу: Get-Service | where name -match "zabbix agent 2" | Restart-Service

### Проверить работу скрипта:
`cd C:\zabbix_agent2-6.2.4\conf\zabbix_agent2.d\scripts\User-Sessions` \
`.\Get-Query-Param.ps1 ACTIVEUSER` \
`.\Get-Query-Param.ps1 INACTIVEUSER` \
`.\Get-Query-Param.ps1 ACTIVECOUNT` \
`.\Get-Query-Param.ps1 INACTIVECOUNT`
