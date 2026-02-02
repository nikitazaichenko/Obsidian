Добавить строчку в файл hosts  
127.0.0.1 genuine-software2.autodesk.com

Добавить запрещающие правила для входящих и исходящих подключений в фаерволл для всех exe по этим путям(включить фаерволл если выключен)  
c:\ProgramData\Autodesk  
c:\Program Files (x86)\Autodesk  
c:\Program Files (x86)\Common Files\Autodesk Shared  
c:\Program Files\Autodesk  
c:\Program Files\Common Files\Autodesk Shared  
c:\Program Files\Common Files\Macrovision Shared\FlexNet

Проще всего через firewall app blocker(\\192.168.50.100\!install\!Utils\fab.zip)

**Для 2019**  
по пути C:\ProgramData\Autodesk\CLM\V7   
Для файла clm-runtime.8b5a4f6393cb942fba1fcda9b1d71984.7.1.326.0.db изменить расширение на .olddb1  
Файл clm-runtime.bb67ffda9cf5515208d42e4680331856.7.1.253.0.db переименовать в clm-runtime.8b5a4f6393cb942fba1fcda9b1d71984.7.1.326.0.db

  
**Для 2020-2024(требует проверки)**  
Откройте C:\ProgramData\Autodesk\CLM\Vxxx и удалите файлы с расширением базы данных — db.