1. Заходим на сервер приложений 1С под локальным админом
2. Запускаем DCOMCNFG  (Консоль настроек "Component  Services")
    1. Открываем ветку Console Root -> Component Services ->  Computers ->  My computer ->  DCOM Config
    2. Ищем "Microsoft Excel Application"
    3. Если нашли, то переходим к пункту 4 (Настраиваем свойства DCOM компонента "Microsoft Excel Application")
    4. Закрываем "Component  Services"
3. Настройка реестра
    1. Запускаем REGEDIT
    2. Открываем ветку Computer\HKEY_CLASSES_ROOT\AppID\EXCEL.EXE, если ее нет, то создаем
    3. Создаем в ней строковый параметр AppID  = {00020812-0000-0000-C000-000000000046}
    4. Выполняем команду "mmc comexp.msc /32", которая делает то же что и DCOMCONFIG, но позволяет видеть  32 битные компоненты.
    5. После этого в Component Services должен появиться "Microsoft Excel Application"
4. Настраиваем свойства DCOM компонента "Microsoft Excel Application"
    1. Закладка "Security"
        1. "Launch and Activation Permissions" - Customize - Edit
            1. Добавляем пользователя, под которым запускается  агент сервера 1С
            2. Назначем ему только следующие права  (allow):
                1. Local Launch
                2. Local Activation
        2. "Access  Permissions" - Customize - Edit
            1. Добавляем пользователя, под которым запускается  агент сервера 1С
            2. Назначаем ему только следующие права  (allow):
                1. Local Access
    2. Закладка "Identity"
        1. Должно быть выбрано "The launching user"
5. Системные папки
    1. Папка "C:\Windows\SysWOW64\config\systemprofile\Desktop\"
        1. Проверяем наличие папки , если нет -то создаем.
        2. Заходим в свойства этой папки.
        3. Закладка Security
        4. Добавляем, если нет, пользователя, под которым запускается агент сервера 1С
        5. Добавляем право "Read" и "Write"
    2. Папка "C:\Windows\System32\config\systemprofile\Desktop\"
        1. Проверяем наличие папки , если нет -то создаем.
        2. Заходим в свойства этой папки.
        3. Закладка Security
        4. Добавляем, если нет, пользователя, под которым запускается агент сервера 1С
        5. Добавляем право "Read" и "Write"