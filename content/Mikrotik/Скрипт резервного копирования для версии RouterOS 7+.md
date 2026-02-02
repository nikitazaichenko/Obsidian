Вставить в System -> Scripts -> Add

Обязательно указать имя бэкапа в теле скрипта, либо в System -> Identity указать имя для распознавания предприятия\устройства резервирования.

{  
:log info "Starting Backup Script...";  
:local sysname [/system identity get name];  
:local sysver [/system package get routeros version];  
:log info "Flushing DNS cache...";  
/ip dns cache flush;  
:delay 2;  
:log info "Deleting last Backups...";  
:foreach i in=[/file find] do={:if ([:typeof [:find [/file get $i name] \  
"$sysname-backup-"]]!="nil") do={/file remove $i}};  
:delay 2;  
:local smtpserv [:resolve "smtp.gmail.com"];  
:local Eaccount [/tool e-mail get user];  
:local pass [/tool e-mail get password];  
:local backupfile ("$sysname-backup-" . \  
[:pick [/system clock get date] 7 11] . [:pick [/system \  
clock get date] 0 3] . [:pick [/system clock get date] 4 6] . ".backup");  
:log info "Creating new Full Backup file...";  
/system backup save name=$backupfile;  
:delay 2;  
:log info "Sending Full Backup file via E-mail...";  
/tool e-mail send from="<$Eaccount>" to=docs@iservice.by server=$smtpserv \  
port=587 user=$Eaccount password=$pass tls=starttls file=$backupfile \  
subject=("$sysname Full Backup **Name(Указать имя)** (" . [/system clock get date] . ")") \  
body=("$sysname full Backup file see in attachment.\nRouterOS version: \  
$sysver\nTime and Date stamp: " . [/system clock get time] . " " . \  
[/system clock get date]);  
:delay 5;  
:log info "All System Backups emailed successfully.\nBackuping completed.";  
}