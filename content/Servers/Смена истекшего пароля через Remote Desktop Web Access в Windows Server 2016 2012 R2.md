[https://winitpro.ru/index.php/2015/02/06/smena-istekshego-parolya-cherez-rds-v-windows-server-2012/](https://winitpro.ru/index.php/2015/02/06/smena-istekshego-parolya-cherez-rds-v-windows-server-2012/)

(ниже приведен урезанный вариант)

В Windows Server 2012 R2 and Windows 8.1 по умолчанию включен механизм аутентификации **NLA** (Network Level Authentication, подробнее о нем [здесь](https://winitpro.ru/index.php/2011/12/26/bezopasnost-sluzhby-remote-desktop-services-v-windows-server-2008-r2/)), который не позволяет подключиться по RDP пользователям [с истекшим сроком действия пароля](https://winitpro.ru/index.php/2020/02/25/ad-user-password-expiration/) (вы, конечно, можете отключить NLA — [ссылка1](https://winitpro.ru/index.php/2018/05/11/rdp-auth-oshibka-credssp-encryption-oracle-remediation/), [ссылка2](https://winitpro.ru/index.php/2014/06/25/windows-2012-rds-ne-podklyuchayutsya-rdp-klienty-windows-xp/), но это не хорошо с точки зрения безопасности). При попытке подключится к серверу RDSH (Remote Desktop Session Host) с учетной записью пользователя, пароль которого истек, появляется такое сообщение об ошибке:

![The Local Security Authority cannot be contacted - This could be due to an expired password](https://winitpro.ru/wp-content/uploads/2015/02/rdp-Local-Security-Authority-cannot-be-contacted.jpg)

В Windows Server 2012 /R2 и выше у удаленных пользователей появилась возможность самостоятельно сбрасывать свой пароль (текущий пароль или пароль с истекшим сроком действия) через специальную веб-страницу на сервере RD Web Access. Процесс смены пароля выглядит так: пользователь заходит под своей учетной записью на веб-страницу регистрации на сервере с ролью RD Web Access и с помощью специальной aspx формы меняет свой пароль.

Чтобы включить функцию смены пароля, нужно на сервере с настроенной ролью Remote Desktop Web Access открыть консоль управления веб-сервером IIS (**IIS** **Manager**), перейти в раздел **[****Server** **Name****] –> Sites** **–> Default** **Web** **Site** **–> RDWeb** **–> Pages** и открыть раздел с настройками приложения (**Application** **Settings**).

[![Sites –> Default Web Site –> RDWeb –> Pages](https://winitpro.ru/wp-content/uploads/2015/02/RDWeb%E2%80%93Pages.jpg)](https://winitpro.ru/wp-content/uploads/2015/02/RDWeb%E2%80%93Pages.jpg)

В правой панели найдите параметр с именем **PasswordChangeEnabled** и измените его значение на **true**.

![PasswordChangeEnabled - опция смены пароля через веб страницу на Remote Desktop Web](https://winitpro.ru/wp-content/uploads/2015/02/PasswordChangeEnabled-rd-web-access.jpg)

Перезапустите IIS из консоли или с помощью команды IISRESET.

Чтобы проверить доступность страницы смены, перейдите на веб-адрес:

https://[RD-WEB-1]/RDWeb/Pages/en-US/password.aspx

Вы можете использовать этот способ смены пароля на **Remote** **Desktop** **Web** **Access** только если на RDWA сервере включена аутентификация **Forms** **Authentication**. При использовании метода **Windows** **Authentication**, смена пароля через форму RD Web невозможна.

Теперь при попытке подключиться к веб серверу RD Web Access с истекшим паролем пользователь будет перенаправлен на веб-страницу password.aspx, на которой ему будет предложено сменить пароль.

[![Необходимо изменить истекший пароль](https://winitpro.ru/wp-content/uploads/2015/02/your-password-is-expired-change-it.jpg)](https://winitpro.ru/wp-content/uploads/2015/02/your-password-is-expired-change-it.jpg)

Вы можете добавить ссылку на страницу с формой смены пароля можно непосредственно в веб-форму входа на сервер RDWeb. Благодаря этому пользователь в любой момент может самостоятельно изменить свой пароль, не дожидаясь окончания его срока действия.

Добавим ссылку на файл password.aspx на страницу входа в систему (создайте копию файла password.aspx перед редактированием)**.**

1. На сервере RDWeb найдите и откройте в любом тестовом редакторе (я предпочитаю Notepad++) файл **C:\Windows\Web\RDWeb\Pages\en-US\login.aspx**
2. Перейдите на **583** строку и вставьте в нее следующий код:  
    `Password Reset Utility`  
    [![Ссылка на страницу смены пароля в login.aspx](https://winitpro.ru/wp-content/uploads/2015/02/change-password-link.jpg)](https://winitpro.ru/wp-content/uploads/2015/02/change-password-link.jpg)
3. Сохраните изменения в файле login.aspx, перезапустите сайт IIS и проверьте что на странице регистрации на терминальном сервере появилась ссылка на страницу смены пароля.

![login.aspx - ссылка на смену пароля пользователя](https://winitpro.ru/wp-content/uploads/2015/02/login.aspx-reset-user-password-web.jpg)